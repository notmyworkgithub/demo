# Demo Guide: Spec-Kit as Enterprise Control Point

## Overview
This demo shows how spec-kit extracts specifications from prototypes, then incorporates corporate controls to create enterprise-ready specifications. The key is showing the **before/after difference** when controls are applied.

## Setup (Before Demo)

1. Have Blue Herald app running locally (or use task 1️⃣ to start it automatically)

2. Have VS Code open with the demo repository

3. Ensure GitHub Copilot is enabled and working

4. **Demo automation is ready**:
   - VS Code tasks provide complete demo automation
   - Access via: `Cmd+Shift+P` → `Tasks: Run Task`
   - Tasks are numbered 0️⃣ through 🔟 for easy sequencing

## Using Demo Tasks

**Task Types**:
- `0️⃣`: Demo overview and workflow summary
- `1️⃣-2️⃣`: Automated setup tasks (run automatically)
- `3️⃣-5️⃣,7️⃣-🔟`: Command display tasks (copy text to Copilot Chat)
- `6️⃣`: Automated file creation task
- `💬`: Demo talking points and key messages

**How to Use**:
1. **Start**: Run `0️⃣ Demo Overview` to see complete workflow
2. **Follow sequence**: Run tasks 1️⃣→2️⃣→3️⃣→...→🔟 in order
3. **Copy commands**: For 📋 tasks, copy displayed text to Copilot Chat
4. **Use talking points**: Follow SAY instructions for smooth presentation

## Demo Flow (45 minutes)

### Phase 1: Demo Setup & Overview (5 minutes)

**Task**: `0️⃣ Demo Overview - Complete Workflow`
**Action**: Shows the complete numbered sequence and timing
**Key Message**: "I'm going to show you how spec-kit serves as a control point between innovation and enterprise deployment"

### Phase 2: Application Setup (5 minutes)

**Task**: `1️⃣ Demo: Start Blue Herald App`
**Action**: Automatically starts the Blue Herald application
**Demo Points**: 
- Show the Policy Update workflow requiring Policy Name + Effective Date
- Demonstrate other communication types briefly
- Point out this was built in hours using vibe-coding

**Task**: `2️⃣ Demo: Initialize Spec-Kit`  
**Action**: Automatically initializes spec-kit in the blue-herald directory
**Key Message**: "Now let's extract specifications from our prototype using spec-kit"

### Phase 3: Specification Extraction (15 minutes)

**Task**: `3️⃣ Demo: Constitution Command (Copy to Copilot Chat)`
**Action**: Displays command to copy into Copilot Chat
**Command**: `/constitution Create basic principles for a communication tool focusing on user experience and functionality`
**Key Message**: "First, let's establish project principles and constraints"

**Task**: `4️⃣ Demo: Analyze App Command (Copy to Copilot Chat)`
**Action**: Displays comprehensive analysis command to copy into Copilot Chat
**Command**: Full `/specify` command with all analysis parameters
**Key Message**: "Now extract exactly what our prototype does"

**Task**: `5️⃣ Demo: Clarify Gaps Command (Copy to Copilot Chat)`
**Action**: Displays clarification command to copy into Copilot Chat
**Command**: `/clarify` command focusing on enterprise deployment gaps
**Key Message**: "Identify what's missing for enterprise deployment"
**Demo Point**: Show the extracted specifications and identified gaps

### Phase 4: Corporate Controls Application (10 minutes)

**Task**: `6️⃣ Demo: Create Corporate Controls Document`
**Action**: Automatically creates corporate-controls.md with enterprise requirements
**Demo Points**:
- Open the created file and show authentication requirements
- Point to approval workflow requirements
- Highlight audit and compliance mandates
**Key Message**: "These are our non-negotiable enterprise requirements"

**Task**: `7️⃣ Demo: Apply Controls Command (Copy to Copilot Chat)`
**Action**: Displays enhancement command to copy into Copilot Chat
**Command**: Complex `/specify` command that preserves business logic while adding controls
**Key Message**: "Apply corporate controls while preserving business logic"

### Phase 5: Implementation Strategy (10 minutes)

**Task**: `8️⃣ Demo: Implementation Plan Command (Copy to Copilot Chat)`
**Action**: Displays plan creation command to copy into Copilot Chat
**Command**: `/plan` command for technical transformation roadmap
**Key Message**: "Create technical roadmap for transformation"

**Task**: `9️⃣ Demo: Development Tasks Command (Copy to Copilot Chat)`
**Action**: Displays task generation command to copy into Copilot Chat
**Command**: `/tasks` command for actionable development steps
**Key Message**: "Generate actionable development tasks"

**Task**: `🔟 Demo: Consistency Analysis Command (Copy to Copilot Chat)`
**Action**: Displays analysis command to copy into Copilot Chat
**Command**: `/analyze` command for quality validation
**Key Message**: "Validate consistency and completeness across all artifacts"

**Demo Points**: Show the complete artifact ecosystem created by spec-kit

### Phase 6: Demo Conclusion (5 minutes)

**Task**: `💬 Demo: Key Messages & Talking Points`
**Action**: Displays all key messages for wrapping up the demo
**Key Messages**:
- "Spec-kit captured exactly what our prototype does - including what it doesn't do for enterprise"
- "These corporate controls are non-negotiable - but we don't want to lose our validated business logic"  
- "Spec-kit created enterprise-ready specifications while preserving every piece of business logic that works"
- **Closing**: "This is the power of spec-kit as a control point - innovate fast, enhance systematically, deploy compliant"

## Quick Reference: Task Sequence

### **Complete Demo Sequence**
Run tasks in this exact order via `Cmd+Shift+P` → `Tasks: Run Task`:

1. **`0️⃣ Demo Overview`** → See complete workflow
2. **`1️⃣ Start Blue Herald App`** → Automated app startup
3. **`2️⃣ Initialize Spec-Kit`** → Automated spec-kit setup
4. **`3️⃣ Constitution Command`** → Copy to Copilot Chat
5. **`4️⃣ Analyze App Command`** → Copy to Copilot Chat
6. **`5️⃣ Clarify Gaps Command`** → Copy to Copilot Chat
7. **`6️⃣ Create Corporate Controls`** → Automated file creation
8. **`7️⃣ Apply Controls Command`** → Copy to Copilot Chat
9. **`8️⃣ Implementation Plan Command`** → Copy to Copilot Chat
10. **`9️⃣ Development Tasks Command`** → Copy to Copilot Chat
11. **`🔟 Consistency Analysis Command`** → Copy to Copilot Chat
12. **`💬 Key Messages & Talking Points`** → Demo conclusion

### **Task Types**
- **🎬 Automated**: Tasks that run commands automatically (1️⃣, 2️⃣, 6️⃣)
- **📋 Copy Tasks**: Tasks that display commands to copy to Copilot Chat (3️⃣-5️⃣, 7️⃣-🔟)
- **🎯 Support**: Overview and talking points (0️⃣, 💬)

### **Demo Timing**
- **Total**: 45 minutes
- **Setup**: 10 minutes (phases 1-2)
- **Extraction**: 15 minutes (phase 3)
- **Controls**: 10 minutes (phase 4)
- **Implementation**: 10 minutes (phase 5)
- **Conclusion**: 5 minutes (phase 6)

## Expected File Outputs

After running the complete demo sequence, you should have:

1. **`constitution.md`** - Project principles and development guidelines
2. **`/specs/001-analyze-current/spec.md`** - Current prototype specifications  
3. **`/specs/001-analyze-current/clarify.md`** - Gap analysis and clarifying questions
4. **`/corporate-controls.md`** - Enterprise governance requirements (auto-created by task 6️⃣)
5. **`/specs/002-enterprise-enhanced/spec.md`** - Enterprise-ready specifications
6. **`/specs/002-enterprise-enhanced/plan.md`** - Technical implementation roadmap
7. **`/specs/002-enterprise-enhanced/tasks.md`** - Actionable development tasks  
8. **`/specs/002-enterprise-enhanced/analyze.md`** - Quality and consistency analysis

## Demo Success Checklist

✅ **All numbered tasks (1️⃣-🔟) completed in sequence**
✅ **Blue Herald app showing Policy Update workflow**
✅ **Spec-kit successfully extracted business logic** 
✅ **Corporate controls document created and displayed**
✅ **Enhanced specifications preserve Policy Update requirements**
✅ **Complete artifact ecosystem generated**
✅ **Clear transformation story demonstrated**

This approach demonstrates spec-kit's complete workflow: **extract → clarify → enhance → plan → execute → validate** while preserving business logic and adding enterprise compliance.