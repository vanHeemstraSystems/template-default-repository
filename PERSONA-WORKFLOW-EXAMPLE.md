# Persona Workflow Example: From PRD to Design

This document demonstrates a complete workflow using AI agent personas in Cursor, from initial product requirements to detailed design specifications.

## Workflow Overview

1. **Product Owner** creates initial PRD
2. **Review and approval** of PRD
3. **Business Analyst** creates detailed design from approved PRD
4. **Security Analyst** creates security assessment from PRD and design
5. **Software Engineer** creates detailed implementation tasks
6. **Scrum Master** creates sprint backlog from implementation tasks
7. **Implementation** by development team

## Step-by-Step Process

### Step 1: Request PRD from Product Owner

In Cursor chat, use this prompt:

```
@product-owner Create a comprehensive PRD for a new user authentication system that includes:
- Social login (Google, GitHub, LinkedIn)
- Traditional email/password registration
- Multi-factor authentication
- Password reset functionality
- User profile management

Please save this PRD to a file called "user-auth-prd.md" in the docs/ directory.
```

**What happens:**
- The Product Owner persona will create a comprehensive PRD
- The AI will automatically save it to `docs/user-auth-prd.md`
- The file will be version-controlled in your repository

### Step 2: Review and Approve the PRD

1. Open the generated `docs/user-auth-prd.md` file
2. Review the content for completeness and accuracy
3. Make any necessary edits or request revisions
4. Once satisfied, proceed to the next step

### Step 3: Business Analyst Creates Design

After approving the PRD, use this prompt:

```
@business-analyst Please review the PRD in docs/user-auth-prd.md and create a detailed technical design document that includes:
- System architecture diagrams
- Database schema design
- API specifications
- User flow diagrams
- Integration requirements
- Test scenarios

Please save this as "user-auth-design.md" in the docs/ directory and reference the original PRD.
```

**What happens:**
- The Business Analyst persona will read the existing PRD file
- Create a comprehensive technical design document
- Save it to `docs/user-auth-design.md`
- Include references to the original PRD

### Step 4: Continue the Workflow

You can then continue with other personas:

```
@software-engineer Review the design in docs/user-auth-design.md and create implementation tasks with technical specifications.
```

```
@security-analyst Review both the PRD and design documents and provide a security assessment with recommendations.
```

## File Organization

Your project structure will look like this:

```
project/
├── docs/
│   ├── user-auth-prd.md          # Product Owner deliverable
│   ├── user-auth-design.md       # Business Analyst deliverable
│   ├── user-auth-security.md     # Security Analyst deliverable
│   ├── user-auth-tasks.md        # Software Engineer deliverable
│   └── user-auth-sprint-backlog.md # Scrum Master deliverable
├── .cursor/
│   └── rules/
│       ├── product-owner.mdc
│       ├── business-analyst.mdc
│       ├── scrum-master.mdc
│       ├── software-engineer.mdc
│       └── security-analyst.mdc
└── PERSONAS.md
```

## Key Benefits

1. **Traceability**: Each document references previous ones
2. **Version Control**: All documents are stored in your repository
3. **Collaboration**: Team members can review and contribute
4. **Consistency**: Each persona follows established frameworks
5. **Handoff**: Clear deliverables between roles

## Pro Tips

### For Better Results:
- **Be Specific**: Provide detailed context about your project
- **Reference Files**: Always mention existing files when building on previous work
- **Iterate**: Ask for revisions if the output doesn't meet your needs
- **Use Context**: Include relevant files using `@filename` in your prompts

### Example Iteration:
```
@product-owner The PRD in docs/user-auth-prd.md needs more detail on the social login providers. Please update it to include specific OAuth flows and error handling requirements.
```

### Cross-Persona Collaboration:
```
@business-analyst Review the PRD in docs/user-auth-prd.md and the security recommendations in docs/user-auth-security.md, then update the design document to incorporate the security requirements.
```

## Sample Prompts for Each Stage

### Initial PRD Creation:
```
@product-owner Create a PRD for [feature description]. Include market research, user stories, success metrics, and technical considerations. Save to docs/[feature-name]-prd.md
```

### Design from PRD:
```
@business-analyst Based on the PRD in docs/[feature-name]-prd.md, create a technical design document with architecture, database design, and API specs. Save to docs/[feature-name]-design.md
```

### Implementation Planning:
```
@software-engineer Review docs/[feature-name]-design.md and break it down into development tasks with technical specifications. Save to docs/[feature-name]-tasks.md
```

### Security Review:
```
@security-analyst Conduct a security assessment of the feature described in docs/[feature-name]-prd.md and docs/[feature-name]-design.md. Save recommendations to docs/[feature-name]-security.md
```

### Sprint Planning:
```
@scrum-master Based on the tasks in docs/[feature-name]-tasks.md, create a sprint plan with story points, dependencies, and timeline. Save to docs/[feature-name]-sprint-plan.md
```

This workflow ensures that each persona builds upon the previous work, creating a comprehensive and traceable development process.
