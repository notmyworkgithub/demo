# Quickstart Guide: Enterprise Employee Announcement Tool

## Overview
This quickstart guide provides step-by-step instructions for setting up and validating the enterprise-ready Employee Announcement Tool with Microsoft 365 integration.

## Prerequisites

### System Requirements
- **Node.js**: 18.x or higher
- **npm**: 9.x or higher
- **Microsoft 365 Tenant**: With SharePoint and Azure AD
- **Azure Subscription**: For Azure SQL and compliance features
- **Development Tools**: VS Code with recommended extensions

### Microsoft 365 Setup
1. **Azure AD App Registration**:
   ```bash
   # Register application in Azure Portal
   # Required permissions: User.Read, Sites.ReadWrite.All, Group.Read.All
   ```

2. **SharePoint Site Collection**:
   - Create dedicated site for Blue Herald
   - Enable SharePoint Framework development
   - Configure custom content types

3. **Security Groups** (Azure AD):
   - `BlueHerald-HRCoordinators`
   - `BlueHerald-HRManagers` 
   - `BlueHerald-Executives`

## Installation

### 1. Clone and Setup
```bash
# Clone repository
git clone <repository-url>
cd blue-herald

# Install dependencies
npm install

# Install SharePoint Framework CLI
npm install -g @microsoft/generator-sharepoint
```

### 2. Environment Configuration
```bash
# Copy environment template
cp .env.example .env.local

# Configure Azure AD settings
REACT_APP_CLIENT_ID=<azure-ad-app-id>
REACT_APP_TENANT_ID=<azure-ad-tenant-id>
REACT_APP_REDIRECT_URI=https://localhost:3000

# Configure SharePoint settings
REACT_APP_SHAREPOINT_SITE=<sharepoint-site-url>
REACT_APP_ANNOUNCEMENTS_LIST=BlueHeraldAnnouncements

# Configure Azure SQL (for audit logs)
AZURE_SQL_CONNECTION_STRING=<connection-string>
```

### 3. SharePoint List Creation
```bash
# Run SharePoint setup script
npm run setup:sharepoint

# This creates:
# - Announcements list with custom content types
# - Approval workflows list
# - User permissions configuration
```

### 4. Database Setup
```bash
# Create Azure SQL audit tables
npm run setup:database

# Run database migrations
npm run db:migrate
```

## Development Workflow

### 1. Start Development Server
```bash
# Start React development server
npm run dev

# Start in SharePoint workbench (for SPFx testing)
npm run serve:spfx
```

### 2. Authentication Flow Testing
```bash
# Test authentication with Azure AD
npm run test:auth

# Verify role-based access
npm run test:rbac
```

### 3. Core Functionality Validation

#### Create Announcement (HR Coordinator)
```javascript
// Test scenario: Create draft announcement
const announcement = {
  title: "New Employee Onboarding Process",
  message: "We're implementing a new onboarding process...",
  communicationType: "PolicyUpdate",
  audience: "AllStaff",
  tone: "Formal",
  additionalFields: {
    policyName: "Employee Onboarding Policy v2.0",
    effectiveDate: "2025-11-01"
  }
};

// Expected: Draft created, audit log entry generated
```

#### Approval Workflow (HR Manager)
```javascript
// Test scenario: Approve policy update
const approvalDecision = {
  announcementId: "announcement-123",
  decision: "Approved",
  rationale: "Policy update aligns with compliance requirements"
};

// Expected: Status changed to Approved, notification sent
```

#### Send Announcement (System)
```javascript
// Test scenario: Send approved announcement
const sendResult = await sendAnnouncement("announcement-123");

// Expected: Status changed to Sent, recipients notified
console.log(`Sent to ${sendResult.recipientCount} recipients`);
```

## Testing Scenarios

### User Story Validation

#### Scenario 1: Policy Update with Approval
```gherkin
Given an HR Coordinator is authenticated
When they create a Policy Update announcement
Then the system displays policy-specific fields
And the announcement enters PendingApproval status
And the manager receives notification

Given a Manager receives approval request
When they approve the announcement
Then the status changes to Approved
And the creator receives notification
And audit logs record the approval

Given an approved Policy Update
When the system sends the announcement
Then recipients receive the formatted announcement
And the status changes to Sent
And audit logs record the send action
```

#### Scenario 2: Real-time Preview
```gherkin
Given a user is creating an announcement
When they select "Urgent" tone
Then the preview updates with red styling
And displays warning emoji prefix
And shows uppercase title formatting

Given a user modifies the message content
When they type in the message field
Then the preview updates immediately
And maintains tone-specific formatting
And preserves existing functionality
```

#### Scenario 3: Role-based Access
```gherkin
Given a user with HRCoordinator role
When they access the approval queue
Then they see only their own submissions
And cannot approve Policy Updates

Given a user with HRManager role
When they access the approval queue
Then they see pending approvals assigned to them
And can approve or reject with rationale

Given a user with Executive role
When they create any announcement type
Then they can send immediately without approval
And bypass standard workflow restrictions
```

### Performance Testing
```bash
# Load testing with concurrent users
npm run test:load -- --users 100 --duration 5m

# SharePoint API performance
npm run test:sharepoint-performance

# Database query performance
npm run test:database-performance
```

### Security Testing
```bash
# Authentication and authorization testing
npm run test:security

# Input validation and XSS prevention
npm run test:input-validation

# HTTPS and secure cookie testing
npm run test:ssl
```

### Compliance Testing
```bash
# WCAG 2.1 accessibility testing
npm run test:accessibility

# Data retention policy testing
npm run test:retention

# Audit log completeness testing
npm run test:audit-completeness
```

## Deployment

### 1. Build Production Assets
```bash
# Build optimized React application
npm run build

# Create SharePoint package
npm run build:spfx

# Generate deployment artifacts
npm run package
```

### 2. SharePoint Deployment
```bash
# Deploy to SharePoint App Catalog
npm run deploy:sharepoint

# Install on target sites
npm run install:sites
```

### 3. Azure Resources
```bash
# Deploy Azure SQL database
npm run deploy:database

# Configure Azure Key Vault
npm run setup:keyvault

# Deploy Azure Functions (if needed)
npm run deploy:functions
```

### 4. Production Validation
```bash
# Smoke tests in production
npm run test:production

# Health check endpoints
curl https://blueherald.sharepoint.com/health

# Audit log validation
npm run validate:audit-logs
```

## Troubleshooting

### Common Issues

#### Authentication Failures
```bash
# Clear MSAL cache
npm run clear:auth-cache

# Verify Azure AD permissions
npm run verify:permissions

# Check token expiration
npm run debug:tokens
```

#### SharePoint Connectivity
```bash
# Test SharePoint API access
npm run test:sharepoint-connection

# Verify list permissions
npm run verify:list-permissions

# Debug CORS issues
npm run debug:cors
```

#### Performance Issues
```bash
# Analyze bundle size
npm run analyze:bundle

# Profile React components
npm run profile:components

# Monitor API response times
npm run monitor:api
```

## Support and Monitoring

### Monitoring Dashboards
- **Azure Application Insights**: Performance and error tracking
- **SharePoint Usage Reports**: User adoption metrics
- **Azure SQL Analytics**: Database performance monitoring

### Support Contacts
- **Technical Issues**: dev@blueherald.com
- **User Training**: training@blueherald.com
- **Security Concerns**: security@blueherald.com

### Documentation Links
- [User Manual](./docs/user-manual.md)
- [Administrator Guide](./docs/admin-guide.md)
- [Security Documentation](./docs/security.md)
- [Compliance Guide](./docs/compliance.md)

## Next Steps

1. **Complete User Acceptance Testing** with HR team
2. **Configure Production Environment** with proper certificates
3. **Setup Monitoring and Alerting** for production issues
4. **Train End Users** on new enterprise features
5. **Establish Support Procedures** for ongoing maintenance

## Success Criteria

✅ **Authentication**: Users can login with Azure AD credentials  
✅ **Authorization**: Role-based access controls function correctly  
✅ **Core Functionality**: All existing announcement features preserved  
✅ **Approval Workflow**: Policy updates require and receive manager approval  
✅ **Audit Logging**: All user actions logged to compliance system  
✅ **Performance**: Page loads under 2 seconds, forms respond under 500ms  
✅ **Security**: HTTPS enabled, input validation active, no security vulnerabilities  
✅ **Compliance**: WCAG 2.1 AA compliance, data retention policies active  
✅ **Integration**: SharePoint and Teams integration working  
✅ **Migration**: Existing data preserved and accessible in new system