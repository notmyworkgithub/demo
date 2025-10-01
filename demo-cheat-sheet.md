# Demo Cheat Sheet - Manual Command Reference

> **PRIMARY METHOD**: Use VS Code numbered tasks (0️⃣-🔟) via `Cmd+Shift+P` → `Tasks: Run Task`
> 
> **BACKUP METHOD**: Use this cheat sheet if tasks aren't available

## Task-Based Demo (Recommended)

**Complete Sequence**: Run these tasks in order:
1. `0️⃣ Demo Overview` → Shows complete workflow
2. `1️⃣ Start Blue Herald App` → Automated startup  
3. `2️⃣ Initialize Spec-Kit` → Automated setup
4. `3️⃣ Constitution Command` → Copy displayed text to Copilot Chat
5. `4️⃣ Analyze App Command` → Copy displayed text to Copilot Chat
6. `5️⃣ Clarify Gaps Command` → Copy displayed text to Copilot Chat
7. `6️⃣ Create Corporate Controls` → Automated file creation
8. `7️⃣ Apply Controls Command` → Copy displayed text to Copilot Chat
9. `8️⃣ Implementation Plan Command` → Copy displayed text to Copilot Chat
10. `9️⃣ Development Tasks Command` → Copy displayed text to Copilot Chat
11. `🔟 Consistency Analysis Command` → Copy displayed text to Copilot Chat
12. `💬 Key Messages & Talking Points` → Demo conclusion

---

## Manual Commands (Backup Reference)

## Terminal Commands (copy and paste into terminal)

```bash
# Initialize spec-kit
cd /Users/t/_repos/demo/blue-herald
specify init . --ai copilot --force
```

## Copilot Chat Commands (copy and paste into Copilot Chat)

### Step 1: Constitution
```
/constitution Create basic principles for a communication tool focusing on user experience and functionality
```

### Step 2: Analyze Current App
```
/specify Analyze this Employee Announcement Tool application and extract comprehensive specifications including:
- All communication types and their required fields
- Business rules for validation
- User workflows and interactions
- Current technical implementation
- Data storage and persistence approach
```

### Step 3: Clarify Enterprise Gaps
```
/clarify Focus on areas that might be unclear for enterprise deployment such as:
- Security and authentication requirements
- Data persistence and storage needs
- Approval and governance workflows
- Integration requirements with enterprise systems
- Scalability and performance considerations
```

### Step 4: Apply Corporate Controls
```
/specify Create an enhanced version of the Employee Announcement Tool that preserves all existing business logic but incorporates the corporate controls from corporate-controls.md. Specifically:

PRESERVE:
- Policy Update workflow requiring Policy Name and Effective Date
- All communication types (Policy Update, Company News, Team Announcement, Benefits Update)
- Dynamic form fields based on communication type
- Real-time preview functionality
- Tone selection and formatting

ADD ENTERPRISE CONTROLS:
- Active Directory authentication with role-based access
- Management approval workflows for Policy Updates
- Complete audit logging for all user actions
- Data retention and compliance features
- Security controls and testing requirements

Generate specifications that show exactly how to transform the prototype into an enterprise-ready application.
```

### Step 5: Create Implementation Plan
```
/plan Create a detailed implementation plan for transforming the current React prototype into an enterprise-ready application that:
- Maintains all existing UI/UX patterns and business logic
- Integrates with Microsoft 365 ecosystem (SharePoint, Teams, Active Directory)
- Implements the corporate controls while preserving user experience
- Provides clear migration strategy from prototype to production
- Includes testing, security, and deployment considerations
```

### Step 6: Generate Tasks
```
/tasks Break down the implementation plan into specific, actionable development tasks that:
- Preserve existing Policy Update business logic
- Add enterprise authentication and authorization
- Implement approval workflows and audit logging
- Integrate with SharePoint for data storage
- Include comprehensive testing strategy
- Address security and compliance requirements
```

### Step 7: Analyze Consistency
```
/analyze Review the specifications, implementation plan, and task list for:
- Consistency between preserved business logic and enhanced requirements
- Coverage of all corporate controls in the implementation approach
- Alignment between user stories and technical tasks
- Completeness of the enterprise transformation strategy
```

## Demo Scripts (use snippets in any text file for these)

Type these in any VS Code file and press Tab:
- `demo-show-app` → Show Blue Herald application script
- `demo-gaps` → Identify enterprise gaps script
- `demo-extracted` → Show extracted specs script
- `demo-controls` → Show corporate controls script
- `demo-results` → Show enhanced results script
- `demo-transformation` → Show complete transformation script
- `demo-messages` → All key talking points

## Quick Copy Commands

**For Terminal:**
- `sk-init` (use snippet in file, then copy result)

**For Copilot Chat:**
- Use the commands above or expand snippets in a file first, then copy

## Demo Flow Summary

**Primary**: Use numbered VS Code tasks for automated demo execution
**Backup**: Use manual commands below if tasks aren't working
**Reference**: Keep this file open during demo for quick command access

## Key Demo Messages

- **Opening**: "I'm going to show you how spec-kit serves as a control point between innovation and enterprise deployment"
- **After extraction**: "Spec-kit captured exactly what our prototype does - including what it doesn't do for enterprise"
- **After controls**: "These corporate controls are non-negotiable - but we don't want to lose our validated business logic"
- **After enhancement**: "Spec-kit created enterprise-ready specifications while preserving every piece of business logic that works"
- **Closing**: "This is the power of spec-kit as a control point - innovate fast, enhance systematically, deploy compliant"