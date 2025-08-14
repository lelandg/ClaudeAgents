# Claude Code Agents

This directory contains specialized agent configurations for Claude Code that extend its capabilities with focused expertise in specific domains. These agents are automatically available in Claude Code and can be invoked using the Task tool.

## Available Agents

Claude Code currently includes 8 specialized agents covering code maintenance, quality assurance, documentation, research, security, performance, testing, and development.

### 1. Code Map Updater (`code-map-updater.md`)
**Model:** Opus  
**Color:** Orange  
**Purpose:** Maintains and updates CodeMap.md documentation files

**Key Capabilities:**
- Checks git history for recent code changes since last update
- Updates class/method inventories with accurate line numbers
- Documents new files and architectural changes
- Maintains hierarchical organization and cross-references
- Follows project-specific documentation standards from CLAUDE_CodeMap.md

**When to Use:**
- After significant code changes or refactoring
- When adding new files or directories to the project
- To update line numbers after code modifications
- To document architectural pattern changes

**Example Usage:**
```
User: "Please update the code map"
Assistant: "I'll use the code-map-updater agent to check for recent changes and update the CodeMap.md file accordingly."
```

### 2. Code Reviewer (`code-reviewer.md`)
**Model:** Opus  
**Color:** Green  
**Purpose:** Reviews code for quality, bugs, performance issues, and best practices

**Key Capabilities:**
- Bug detection (logic errors, edge cases, resource leaks, security issues)
- Code quality analysis (SOLID principles, design patterns, maintainability)
- Performance review (algorithm efficiency, bottlenecks, memory usage)
- Best practices compliance (language idioms, project standards)
- Provides specific, actionable improvement suggestions

**Review Structure:**
1. Summary overview
2. Critical issues (must fix)
3. Important suggestions (quality/performance)
4. Minor suggestions (style/optimization)
5. Positive observations

**When to Use:**
- After implementing new features or functions
- Following code refactoring
- When explicitly requested for code review
- Automatically after writing significant code blocks

**Example Usage:**
```
User: "I've refactored the mesh generation pipeline. Can you check if it looks good?"
Assistant: "I'll use the code-reviewer agent to thoroughly review your refactored mesh generation pipeline."
```

### 3. Documentation Specialist (`documentation-specialist.md`)
**Model:** Sonnet  
**Color:** Blue  
**Purpose:** Creates and maintains comprehensive technical documentation

**Key Capabilities:**
- Creates user guides, API docs, developer documentation
- Writes README files and architecture documents
- Updates documentation to match code changes
- Provides clear examples and troubleshooting guides
- Tailors content for different audiences (users vs developers)

**Documentation Types:**
- README files with quick start guides
- API documentation with endpoints and parameters
- Architecture documents explaining system design
- User guides with tutorials
- Developer setup and contribution guidelines
- Configuration documentation
- Migration and upgrade guides
- Troubleshooting guides and FAQs

**When to Use:**
- After implementing new features requiring documentation
- When existing documentation needs updating
- To create API or user documentation from scratch
- When code changes require documentation updates

**Example Usage:**
```
User: "I just added a new authentication system to the project. Can you document it?"
Assistant: "I'll use the documentation-specialist agent to create comprehensive documentation for your new authentication system."
```

### 4. Research Assistant (`research-assistant.md`)
**Model:** Sonnet  
**Color:** Yellow  
**Purpose:** Researches technologies, best practices, and implementation approaches

**Key Capabilities:**
- Investigates multiple implementation approaches
- Compares technologies with pros/cons analysis
- Provides code examples and practical guidance
- Recommends solutions based on project context
- Synthesizes information from multiple sources

**Research Methodology:**
1. Clarifies scope and requirements
2. Systematic analysis of options
3. Practical implementation focus
4. Clear decision framework
5. Actionable recommendations

**When to Use:**
- Exploring new technologies or frameworks
- Comparing different implementation approaches
- Understanding new features or APIs
- Making architectural decisions
- Investigating best practices for specific scenarios

**Example Usage:**
```
User: "Should I use PostgreSQL or MongoDB for my new project?"
Assistant: "Let me use the research-assistant agent to research and compare these database options for your use case."
```

### 5. Security Auditor (`security-auditor.md`)
**Model:** Opus  
**Color:** Red  
**Purpose:** Performs comprehensive security audits to identify vulnerabilities and ensure security best practices

**Key Capabilities:**
- OWASP Top 10 vulnerability detection (injection, XSS, broken auth, etc.)
- Secret detection (API keys, passwords, credentials)
- Authentication & authorization review
- Input validation and sanitization checking
- Cryptography assessment and security header validation
- Dependency vulnerability scanning (CVE checking)

**Security Focus Areas:**
1. Vulnerability detection and classification
2. Secret and credential scanning
3. Authentication/authorization analysis
4. Input validation verification
5. Security configuration review

**When to Use:**
- After implementing authentication or security-sensitive features
- Before production deployments
- When handling user input or sensitive data
- For periodic security audits
- When concerned about specific vulnerabilities

**Example Usage:**
```
User: "Can you check if my authentication code is secure?"
Assistant: "I'll use the security-auditor agent to analyze your authentication implementation for vulnerabilities."
```

### 6. Performance Optimizer (`performance-optimizer.md`)
**Model:** Opus  
**Color:** Yellow  
**Purpose:** Analyzes code performance, identifies bottlenecks, and suggests optimizations

**Key Capabilities:**
- Algorithmic complexity analysis (time/space)
- Database query optimization and indexing strategies
- Frontend rendering and loading performance
- Backend application and API performance
- Caching strategy implementation
- Memory leak and resource usage detection

**Optimization Areas:**
1. Algorithm efficiency improvements
2. Database query optimization
3. Caching implementation
4. Async operation optimization
5. Resource management

**When to Use:**
- When application is running slowly
- After implementing complex algorithms
- For database-heavy operations
- Before scaling applications
- When optimizing critical paths

**Example Usage:**
```
User: "My application is running slowly, can you help optimize it?"
Assistant: "I'll use the performance-optimizer agent to analyze your code and identify performance bottlenecks."
```

### 7. Test Generator (`test-generator.md`)
**Model:** Sonnet  
**Color:** Purple  
**Purpose:** Creates comprehensive test suites to ensure code quality and reliability

**Key Capabilities:**
- Unit test generation with edge cases
- Integration and end-to-end test creation
- Mock and fixture generation
- Test coverage analysis and improvement
- Framework-specific test patterns (Jest, pytest, JUnit, etc.)
- Edge case and boundary condition identification

**Test Generation Focus:**
1. Comprehensive unit tests
2. Integration test scenarios
3. Mock and stub creation
4. Edge case coverage
5. Test organization and structure

**When to Use:**
- After implementing new features or functions
- To improve test coverage
- When refactoring requires test updates
- For critical business logic
- To establish testing baselines

**Example Usage:**
```
User: "Can you write tests for the UserService class?"
Assistant: "I'll use the test-generator agent to create comprehensive tests for the UserService class."
```

### 8. Software Engineer (`software-engineer.md`)
**Model:** Opus  
**Color:** Purple  
**Purpose:** Writes new code, fixes bugs, implements features, and refactors existing code

**Key Capabilities:**
- New feature implementation
- Bug fixing and debugging
- Code refactoring and optimization
- Algorithm development
- API endpoint creation
- Design pattern implementation

**Development Approach:**
- Requirements clarification
- System context consideration
- Integrated solution design
- Edge case handling
- Quality code production

**When to Use:**
- Implementing new features
- Fixing bugs or errors
- Refactoring existing code
- Creating new modules or classes
- Solving complex programming problems

**Example Usage:**
```
User: "Implement a caching mechanism for the API"
Assistant: "I'll use the software-engineer agent to implement a robust caching mechanism for your API."
```

## Agent Configuration Format

Each agent file follows a YAML frontmatter format:

```yaml
---
name: agent-name
description: Detailed description with examples
tools: List of available tools (optional)
model: claude model to use (opus/sonnet)
color: UI color for the agent
---

[Agent prompt and instructions]
```

## How Agents Work

1. **Invocation**: Agents are invoked through Claude Code's Task tool
2. **Stateless Execution**: Each agent invocation is independent
3. **Specialized Expertise**: Agents have focused prompts for specific domains
4. **Tool Access**: Agents can use various tools (Read, Write, Edit, Bash, etc.)
5. **Automatic Selection**: Claude Code selects appropriate agents based on task context

## Best Practices

1. **Let Claude Code choose**: Claude Code will automatically select the appropriate agent based on your request
2. **Be specific**: Provide clear context about what you need
3. **Review outputs**: Agent suggestions should be reviewed before implementation
4. **Chain agents**: Multiple agents can be used sequentially for complex tasks
5. **Provide context**: Include relevant project information for better results

## Creating Custom Agents

To create a new agent:

1. Create a new `.md` file in this directory
2. Add YAML frontmatter with required fields
3. Write the agent's prompt and instructions
4. The agent will be automatically available in Claude Code

## Notes

- Agents are designed to be proactive when appropriate
- Some agents (like code-reviewer) may be invoked automatically after certain actions
- Agents follow project-specific standards from CLAUDE.md files when available
- Each agent has access to specific tools optimized for their purpose