# AI Agent Personas in Cursor

This guide explains how to use AI agent personas in Cursor, similar to GitHub Copilot's persona dropdown functionality.

## What are AI Agent Personas?

AI Agent Personas are specialized AI agents designed for specific work tasks and roles. Each persona includes detailed instructions, capabilities, and examples to help AI systems perform targeted professional functions like creating Product Requirement Documents, analyzing business requirements, or conducting technical reviews.

## How Cursor Personas Work

Unlike GitHub Copilot's dropdown menu, Cursor uses a **Rules** system to implement personas. Each persona is stored as a `.mdc` file in the `.cursor/rules` directory and can be activated using the `@` symbol in chat.

## Available Personas

### Product Owner (`@product-owner`)
- **Purpose**: Creates Product Requirement Documents (PRDs) and manages product strategy
- **Key Deliverables**: PRDs, User Stories, Product Roadmaps, Feature Specifications
- **Best For**: Product planning, feature definition, stakeholder communication

### Business Analyst (`@business-analyst`)
- **Purpose**: Analyzes requirements and creates technical specifications
- **Key Deliverables**: BRDs, Functional Specifications, Process Flow Diagrams, Use Cases
- **Best For**: Requirements gathering, process analysis, gap analysis

### Scrum Master (`@scrum-master`)
- **Purpose**: Facilitates agile processes and removes impediments
- **Key Deliverables**: Sprint Planning Agendas, Retrospective Action Items, Team Velocity Reports
- **Best For**: Agile facilitation, team coaching, process optimization

### Software Engineer (`@software-engineer`)
- **Purpose**: Designs, develops, and maintains software systems
- **Key Deliverables**: Technical Design Documents, Code Implementation, API Documentation
- **Best For**: Software development, system architecture, code reviews

### Security Analyst (`@security-analyst`)
- **Purpose**: Conducts security assessments and implements security measures
- **Key Deliverables**: Security Assessment Reports, Threat Modeling Reports, Incident Response Plans
- **Best For**: Security assessments, vulnerability analysis, compliance management

## How to Use Personas

### Method 1: Manual Activation with @ Symbol
In any Cursor chat, type `@` followed by the persona name to activate it:

```
@product-owner Create a PRD for a new user authentication feature
```

```
@business-analyst Analyze the requirements for our inventory management system
```

```
@scrum-master Plan a sprint retrospective for our development team
```

```
@software-engineer Review this code for performance and security issues
```

```
@security-analyst Conduct a threat assessment for our web application
```

### Method 2: Settings Panel
1. Open **Cursor Settings** (Cmd/Ctrl + ,)
2. Go to **Rules** section
3. You'll see all available personas listed
4. Click on a persona to view its details
5. Use the persona by referencing it with `@` in chat

### Method 3: Command Palette
1. Open Command Palette (Cmd/Ctrl + Shift + P)
2. Type "Cursor Rules" to see rule-related commands
3. Select the persona you want to use

## Creating New Personas

### Step 1: Create the Rule File
Create a new `.mdc` file in `.cursor/rules/`:

```bash
.cursor/rules/your-persona-name.mdc
```

### Step 2: Use the Persona Template
```markdown
---
description: [Brief description of the persona's role]
globs: []
alwaysApply: false
---

# [Persona Name] AI Agent

You are [role description with experience level].

## Core Capabilities
- Capability 1
- Capability 2
- Capability 3

## Key Deliverables
- Document Type 1
- Document Type 2
- Process/Framework 3

## Communication Style
[Description of how this persona communicates]

## Domain Expertise
- Area 1
- Area 2
- Area 3

## Always Remember
- Key principle 1
- Key principle 2
- Key principle 3
```

### Step 3: Test Your Persona
Use `@your-persona-name` in chat to test the new persona.

## Best Practices

### For Using Personas
1. **Be Specific**: Provide clear context about your project and requirements
2. **Use Examples**: Reference existing documents or similar projects when possible
3. **Iterate**: Refine the output by asking follow-up questions
4. **Combine Personas**: Use different personas for different aspects of the same project

### For Creating Personas
1. **Keep Focused**: Each persona should have a clear, specific role
2. **Include Examples**: Provide sample prompts and expected outputs
3. **Be Detailed**: Include specific frameworks, methodologies, and best practices
4. **Test Thoroughly**: Validate the persona with real-world scenarios

## Example Workflows

### Complete Product Development Workflow
1. **Discovery**: `@product-owner Create a PRD for [feature] with market research and user stories`
2. **Technical Design**: `@business-analyst Create technical design based on the PRD`
3. **Security Assessment**: `@security-analyst Review PRD and design for security requirements`
4. **Implementation Planning**: `@software-engineer Create detailed technical tasks`
5. **Sprint Planning**: `@scrum-master Create sprint backlog from implementation tasks`
6. **Development**: Execute sprints with regular ceremonies and reviews

### Requirements Analysis Workflow
1. **Initial Analysis**: `@business-analyst Document current state of [process]`
2. **Gap Analysis**: `@business-analyst Identify gaps between current and desired state`
3. **Solution Design**: `@product-owner Define product requirements to address gaps`
4. **Security Review**: `@security-analyst Assess security implications`
5. **Implementation Planning**: `@software-engineer Break down into technical tasks`
6. **Sprint Organization**: `@scrum-master Organize tasks into manageable sprints`

## Troubleshooting

### Persona Not Working?
- Ensure the `.mdc` file is in `.cursor/rules/` directory
- Check that the file has proper MDC format with metadata header
- Verify the persona name matches the filename (without .mdc extension)
- Try restarting Cursor if the persona doesn't appear

### Persona Not Behaving as Expected?
- Review the persona definition for clarity and completeness
- Add more specific examples and constraints
- Test with different types of prompts
- Refine the communication style and domain expertise sections

## Advanced Features

### Conditional Activation
Use `globs` to automatically activate personas based on file types:
```yaml
---
description: Frontend Developer
globs: ["*.tsx", "*.jsx", "*.css"]
alwaysApply: false
---
```

### Always Active Personas
Set `alwaysApply: true` to make a persona always active (use sparingly):
```yaml
---
description: Code Style Guide
globs: []
alwaysApply: true
---
```

## Tips for Success

1. **Start Simple**: Begin with basic personas and gradually add complexity
2. **Document Everything**: Keep track of which personas work best for which tasks
3. **Share with Team**: Version control your `.cursor/rules` directory to share personas
4. **Regular Updates**: Refine personas based on usage and feedback
5. **Combine with Context**: Use personas alongside Cursor's other context features (@files, @docs, etc.)

## Comparison with GitHub Copilot

| Feature | GitHub Copilot | Cursor |
|---------|----------------|---------|
| Activation | Dropdown menu | `@persona-name` |
| Storage | Cloud-based | Local `.cursor/rules` files |
| Customization | Limited | Full control over persona definition |
| Version Control | No | Yes (files are in your repo) |
| Team Sharing | Automatic | Via version control |
| Complexity | Simple | Advanced (supports conditions, globs, etc.) |

While Cursor doesn't have a dropdown menu like Copilot, its Rules system is more powerful and flexible, allowing for highly customized personas that can be version-controlled and shared with your team.
