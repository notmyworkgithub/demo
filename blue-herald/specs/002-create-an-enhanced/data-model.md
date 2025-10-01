# Data Model: Enterprise Employee Announcement Tool

## Core Entities

### Announcement
**Purpose**: Core communication entity with enterprise controls and audit trail

**Attributes**:
- `id`: Unique identifier (SharePoint List Item ID)
- `title`: Announcement title (required, max 200 chars)
- `message`: Announcement content (required, rich text)
- `communicationType`: Enum (PolicyUpdate, CompanyNews, TeamAnnouncement, BenefitsUpdate)
- `audience`: Enum (AllStaff, Department, Team)
- `tone`: Enum (Formal, Friendly, Urgent, Celebratory)
- `status`: Enum (Draft, PendingApproval, Approved, Rejected, Sent, Archived)
- `createdBy`: User reference (Azure AD UPN)
- `createdDate`: Timestamp (ISO 8601)
- `modifiedBy`: User reference (Azure AD UPN)
- `modifiedDate`: Timestamp (ISO 8601)
- `approvedBy`: User reference (Azure AD UPN, nullable)
- `approvedDate`: Timestamp (ISO 8601, nullable)
- `sentDate`: Timestamp (ISO 8601, nullable)
- `retentionDate`: Calculated date for compliance archival
- `legalHold`: Boolean flag for litigation support

**Relationships**:
- One-to-Many with AnnouncementAuditLog
- One-to-One with ApprovalWorkflow (for PolicyUpdate type)
- One-to-Many with AdditionalFields

**Validation Rules**:
- Title and message are required for all types
- PolicyUpdate requires approvedBy before sentDate can be set
- RetentionDate calculated based on communicationType and compliance policies
- Status transitions must follow workflow: Draft → PendingApproval → Approved → Sent → Archived

**State Transitions**:
```
Draft → PendingApproval (when PolicyUpdate submitted)
PendingApproval → Approved (manager approval)
PendingApproval → Rejected (manager rejection)
Approved → Sent (system sends announcement)
Sent → Archived (retention period expired, unless legalHold = true)
```

### User
**Purpose**: Enhanced user entity with role-based permissions and organizational hierarchy

**Attributes**:
- `upn`: Azure AD User Principal Name (primary key)
- `displayName`: Full name from Azure AD
- `email`: Email address from Azure AD
- `roles`: Array of application roles (HRCoordinator, HRManager, Executive)
- `department`: Department from Azure AD
- `managerId`: Manager UPN from Azure AD organizational hierarchy
- `isActive`: Boolean status
- `lastLoginDate`: Timestamp for audit purposes
- `permissionLevel`: Calculated field based on roles

**Relationships**:
- One-to-Many with Announcement (as creator)
- One-to-Many with ApprovalWorkflow (as approver)
- Hierarchical relationship (manager-direct report)

**Derived Permissions**:
- **HRCoordinator**: Create announcements, view own submissions
- **HRManager**: Create and approve PolicyUpdates, view team submissions
- **Executive**: Create and send all types without approval, view all announcements

### ApprovalWorkflow
**Purpose**: Manages approval process for PolicyUpdate announcements

**Attributes**:
- `id`: Unique identifier
- `announcementId`: Reference to Announcement
- `requestedBy`: User UPN who submitted for approval
- `requestedDate`: Timestamp of submission
- `assignedTo`: Manager UPN for approval
- `status`: Enum (Pending, Approved, Rejected, Escalated)
- `decision`: Approval or rejection decision
- `decisionRationale`: Manager's reason for decision (required for rejection)
- `decisionDate`: Timestamp of manager decision
- `escalatedTo`: Senior manager UPN (if original manager unavailable)
- `escalationDate`: Timestamp of escalation
- `expirationDate`: Auto-escalation date (7 days from request)

**Relationships**:
- One-to-One with Announcement
- Many-to-One with User (assignedTo)
- One-to-Many with WorkflowAuditLog

**Business Rules**:
- Only PolicyUpdate announcements require approval
- Manager assignment based on organizational hierarchy
- Auto-escalation after 7 days without decision
- Decision rationale required for rejections

### AdditionalFields
**Purpose**: Communication type-specific data fields

**Attributes**:
- `id`: Unique identifier
- `announcementId`: Reference to Announcement
- `fieldName`: String (policyName, effectiveDate, newsCategory, etc.)
- `fieldValue`: String value
- `fieldType`: Enum (Text, Date, Selection)
- `isRequired`: Boolean

**Type-Specific Fields**:

**PolicyUpdate**:
- `policyName`: Text (required)
- `effectiveDate`: Date (required)

**CompanyNews**:
- `newsCategory`: Selection (ProductLaunch, CompanyGrowth, Awards, Partnership, Other)
- `impactLevel`: Selection (AllEmployees, SpecificDepartments, Leadership, Customers)

**TeamAnnouncement**:
- `teamName`: Text (required)
- `announcementType`: Selection (NewTeamMember, ProjectUpdate, ProcessChange, Achievement, Meeting)

**BenefitsUpdate**:
- `benefitType`: Selection (HealthInsurance, RetirementPlan, PTOPolicy, Wellness, ProfessionalDevelopment)
- `enrollmentDeadline`: Date (required)

### AnnouncementAuditLog
**Purpose**: Comprehensive audit trail for compliance and security monitoring

**Attributes**:
- `id`: Unique identifier
- `announcementId`: Reference to Announcement (nullable for system events)
- `userId`: User UPN performing action
- `action`: Enum (Created, Modified, Submitted, Approved, Rejected, Sent, Viewed, Deleted)
- `timestamp`: Timestamp (ISO 8601)
- `ipAddress`: Client IP address
- `userAgent`: Browser/client information
- `previousValues`: JSON object with before state
- `newValues`: JSON object with after state
- `sessionId`: Browser session identifier
- `correlationId`: Request correlation for tracing

**Relationships**:
- Many-to-One with Announcement
- Many-to-One with User

**Retention Policy**:
- Audit logs retained for 7 years minimum
- Compliance exports available for legal discovery
- Real-time streaming to Azure Sentinel for security monitoring

### Permission
**Purpose**: Role-based access control matrix

**Attributes**:
- `role`: Enum (HRCoordinator, HRManager, Executive)
- `resource`: String (Announcement, ApprovalWorkflow, AuditLog)
- `action`: Enum (Create, Read, Update, Delete, Approve, Send)
- `allowed`: Boolean

**Permission Matrix**:
```
HRCoordinator:
- Announcement: Create, Read (own), Update (own drafts)
- ApprovalWorkflow: Read (own submissions)

HRManager:
- Announcement: Create, Read (team), Update (own drafts), Approve (PolicyUpdates)
- ApprovalWorkflow: Read, Approve, Reject
- AuditLog: Read (team activities)

Executive:
- Announcement: Create, Read (all), Update (own), Send (all types)
- ApprovalWorkflow: Read (all), Override
- AuditLog: Read (department activities)
```

## Data Storage Architecture

### SharePoint Lists
**Announcements List**:
- Custom content types for each communication type
- Lookup columns for user references
- Calculated columns for status and retention dates
- Workflow integration with Power Automate

**Approval Workflows List**:
- Workflow history and status tracking
- Integration with SharePoint approval workflows
- Email notifications for pending approvals

### Azure SQL Database
**Audit Tables**:
- High-performance audit log storage
- Partitioned by date for optimal querying
- Encrypted at rest with Azure Key Vault integration
- Automated backup and disaster recovery

### Microsoft Graph Integration
**User Profiles**:
- Real-time sync with Azure AD
- Organizational hierarchy mapping
- Role assignments from security groups
- Profile picture and presence information

## Migration Strategy

### Phase 1: Data Structure Setup
1. Create SharePoint lists with custom content types
2. Configure Azure SQL audit database
3. Set up Microsoft Graph API permissions
4. Implement data access layer

### Phase 2: Data Migration
1. Export existing announcement data (if any)
2. Import into SharePoint with audit trail creation
3. Validate data integrity and relationships
4. Test backup and recovery procedures

### Phase 3: Integration Testing
1. End-to-end data flow testing
2. Performance testing with production data volumes
3. Security and compliance validation
4. Disaster recovery testing