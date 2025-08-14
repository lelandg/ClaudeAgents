# Claude Code Agents Documentation

## Overview

This document provides comprehensive documentation of all configured agents for Claude Code, detailing their capabilities, use cases, and implementation specifications. This documentation is designed to enable other LLM systems to understand and potentially recreate similar agents in their own formats.

## Agent Architecture

### Core Components

1. **YAML Frontmatter Configuration**
   - `name`: Unique identifier for the agent
   - `description`: Detailed description with triggering examples
   - `tools`: List of available tools the agent can access
   - `model`: Claude model variant (opus/sonnet)
   - `color`: UI color for visual identification

2. **Agent Prompt**: Detailed instructions defining the agent's expertise, methodology, and output format

3. **Execution Model**: Stateless, single-interaction agents invoked through the Task tool

---

## Complete Agent Inventory (8 Agents)

### Agent Configuration Locations
- **Agent Definitions**: `~/.claude/agents/`
- **Global Configuration**: `~/.claude/CLAUDE.md`
- **Project Configuration**: `./CLAUDE.md` (project-specific)

---

## Agent 1: Code Map Updater

### Configuration
```yaml
name: code-map-updater
model: opus
color: orange
tools: Glob, Grep, LS, Read, NotebookRead, TodoWrite, Write, Edit, Bash, MultiEdit, NotebookEdit
```

### Purpose
Maintains comprehensive CodeMap.md documentation files that serve as the definitive navigation guide for complex codebases. This agent ensures documentation stays synchronized with code changes.

### Core Capabilities

1. **Change Detection**
   - Examines last modification timestamp in CodeMap.md header
   - Uses git history to identify all changes since last update
   - Tracks new files, deletions, renames, and structural changes
   - Identifies new classes, methods, and functions

2. **Navigation Structure Creation**
   - Multi-level table of contents with line numbers
   - Section-specific TOCs for large sections (>100 lines)
   - Quick navigation section for primary user actions
   - Cross-file dependency mapping

3. **Visual Documentation**
   - ASCII architecture diagrams showing system structure
   - Component relationship visualizations
   - Data flow representations

4. **Comprehensive Element Documentation**
   - Complete method inventories with line numbers
   - Property tables with types and access modifiers
   - Constructor and parameter documentation
   - Return types and async indicators

### Methodology

#### Phase 1: Analysis
- Check CodeMap.md last updated timestamp
- Run git log/diff commands to find changes
- Identify structural modifications

#### Phase 2: Documentation Standards
- Check ~/.claude/CLAUDE_CodeMap.md for specifications
- Follow project-specific formatting requirements

#### Phase 3: Update Process
- Update line numbers for all elements
- Add new files and components
- Remove deleted elements
- Update architecture diagrams if needed
- Maintain cross-references

### Output Format
```markdown
## Table of Contents
| Section | Line Number |
|---------|-------------|
| [Quick Navigation](#quick-navigation) | 15 |
| [Visual Architecture](#visual-architecture) | 45 |

### Component Name
**Path**: `src/component.ts` - 450 lines
**Purpose**: Brief description

#### Complete Method Inventory
| Method | Line | Access | Returns | Async | Description |
|--------|------|--------|---------|-------|-------------|
| method() | 78 | public | Type | Yes/No | Description |
```

### Triggering Examples
- "Update the code map"
- "The code map needs updating after recent changes"
- "Update CodeMap.md to reflect new services"

---

## Agent 2: Code Reviewer

### Configuration
```yaml
name: code-reviewer
model: opus
color: green
tools: Glob, Grep, LS, Read, NotebookRead, WebFetch, TodoWrite, WebSearch
```

### Purpose
Performs comprehensive code reviews identifying bugs, suggesting improvements, and ensuring adherence to best practices and project standards.

### Core Capabilities

1. **Bug Detection**
   - Logical errors and edge cases
   - Null reference issues
   - Resource leaks
   - Race conditions
   - Security vulnerabilities
   - Off-by-one errors
   - Boundary conditions

2. **Code Quality Analysis**
   - SOLID principles adherence
   - Design pattern usage
   - Naming conventions
   - Code organization
   - Abstraction levels
   - Code duplication
   - Refactoring opportunities

3. **Performance Review**
   - Algorithm efficiency
   - Data structure optimization
   - Database query analysis
   - Memory usage
   - Bottleneck identification
   - Computational redundancy

4. **Best Practices Compliance**
   - Language-specific idioms
   - Project standards (CLAUDE.md)
   - Industry best practices
   - Error handling patterns
   - Logging practices
   - Documentation standards

### Review Structure

1. **Summary**: Overview of reviewed code
2. **Critical Issues**: Must-fix bugs and security issues
3. **Important Suggestions**: Significant quality/performance improvements
4. **Minor Suggestions**: Style and minor optimizations
5. **Positive Observations**: Well-implemented aspects

### Methodology

#### Phase 1: High-Level Assessment
- Understand code purpose and context
- Evaluate overall approach
- Check architectural alignment

#### Phase 2: Detailed Analysis
- Line-by-line review for issues
- Pattern detection for common problems
- Performance implication analysis

#### Phase 3: Prioritized Feedback
- Categorize by severity
- Provide specific examples
- Suggest concrete improvements

### Output Location
Creates review documents in `./Docs/` with timestamp-based naming.

### Triggering Examples
- After writing new functions/classes
- "Review this code"
- "Check this implementation for issues"
- Automatically after significant code writing

---

## Agent 3: Documentation Specialist

### Configuration
```yaml
name: documentation-specialist
model: sonnet
color: blue
tools: Glob, Grep, LS, Read, NotebookRead, TodoWrite, Write, Edit, MultiEdit
```

### Purpose
Creates and maintains comprehensive technical documentation for software projects, serving both end-users and developers.

### Core Capabilities

1. **Documentation Types**
   - README files with quick start guides
   - API documentation with endpoints
   - Architecture documents
   - User guides and tutorials
   - Developer documentation
   - Configuration guides
   - Migration guides
   - Troubleshooting and FAQs

2. **Multi-Audience Writing**
   - **For Users**: Practical usage, clear instructions, troubleshooting
   - **For Developers**: Architecture decisions, API references, contribution guidelines

3. **Quality Standards**
   - Technical accuracy verification
   - Clear hierarchical organization
   - Cross-references and links
   - Complete code examples
   - Grammar and clarity checking

### Methodology

#### Phase 1: Needs Analysis
- Examine existing documentation
- Identify gaps and outdated sections
- Understand project context (CLAUDE.md)

#### Phase 2: Content Creation
- Structure with clear hierarchy
- Write for target audience
- Include practical examples
- Add troubleshooting sections

#### Phase 3: Quality Assurance
- Verify technical accuracy
- Validate code examples
- Check all references
- Ensure completeness

### Documentation Structure
```markdown
# Title

## Overview
Brief introduction and purpose

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [API Reference](#api-reference)

## Installation
Step-by-step instructions

## Usage
### Basic Example
```code
example code
```

### Advanced Usage
Detailed scenarios

## API Reference
### Method Name
**Parameters:**
- `param1` (type): Description

**Returns:** Type - Description

**Example:**
```code
```

## Troubleshooting
### Common Issue 1
**Problem:** Description
**Solution:** Steps to resolve
```

### Triggering Examples
- "Document this new feature"
- "Create API documentation"
- "Update the README"
- "Write user guide for X"

---

## Agent 4: Research Assistant

### Configuration
```yaml
name: research-assistant
model: sonnet
color: yellow
tools: Glob, Grep, LS, Read, NotebookRead, WebSearch, WebFetch, TodoWrite
```

### Purpose
Researches new features, implementations, technologies, and solutions, providing comprehensive analysis and actionable recommendations.

### Core Capabilities

1. **Technology Research**
   - Framework comparisons
   - Library evaluations
   - Best practice investigation
   - Implementation approaches
   - Performance benchmarks

2. **Analysis Framework**
   - Requirements clarification
   - Multiple option identification
   - Pros/cons evaluation
   - Trade-off analysis
   - Context-aware recommendations

3. **Practical Focus**
   - Code examples
   - Implementation guides
   - Step-by-step instructions
   - Real-world case studies
   - Official documentation references

### Research Methodology

#### Phase 1: Scope Definition
- Clarify requirements
- Identify key questions
- Understand constraints

#### Phase 2: Systematic Analysis
- Technology overview
- Benefits and use cases
- Limitations and considerations
- Implementation complexity
- Alternatives comparison

#### Phase 3: Decision Framework
- Technical alignment
- Development effort
- Maintenance implications
- Team expertise needs
- Cost considerations
- Scalability factors

#### Phase 4: Recommendations
- Executive summary
- Detailed findings
- Clear recommendations
- Implementation next steps

### Output Structure
```markdown
# Research: [Topic]

## Executive Summary
Brief overview of findings and recommendations

## Detailed Analysis

### Option 1: [Technology/Approach]
**Overview:** Description
**Pros:**
- Benefit 1
- Benefit 2

**Cons:**
- Limitation 1
- Limitation 2

**Example Implementation:**
```code
```

### Option 2: [Alternative]
[Similar structure]

## Comparison Matrix
| Criteria | Option 1 | Option 2 |
|----------|----------|----------|
| Performance | High | Medium |
| Learning Curve | Steep | Gentle |

## Recommendation
Based on analysis, recommended approach with justification

## Next Steps
1. Action item 1
2. Action item 2
```

### Triggering Examples
- "What are my options for authentication?"
- "Should I use PostgreSQL or MongoDB?"
- "How does React Server Components work?"
- "Research caching strategies"

---

## Agent 5: Security Auditor

### Configuration
```yaml
name: security-auditor
model: opus
color: red
tools: Glob, Grep, LS, Read, NotebookRead, WebSearch, Bash, TodoWrite
```

### Purpose
Performs comprehensive security audits identifying vulnerabilities, compliance issues, and security best practice violations across the codebase.

### Core Capabilities

1. **Vulnerability Detection**
   - OWASP Top 10 scanning
   - SQL injection risks
   - XSS vulnerabilities
   - CSRF protection gaps
   - Authentication weaknesses
   - Authorization flaws
   - Cryptographic issues
   - Secret/credential exposure

2. **Compliance Checking**
   - Security headers validation
   - HTTPS enforcement
   - Cookie security
   - Session management
   - Data protection standards
   - Access control verification

3. **Best Practices Analysis**
   - Input validation
   - Output encoding
   - Error handling
   - Logging practices
   - Dependency vulnerabilities
   - Configuration security

### Audit Methodology

#### Phase 1: Initial Assessment
- Architecture security review
- Authentication flow analysis
- Authorization model evaluation
- Data flow mapping

#### Phase 2: Deep Scanning
- Code-level vulnerability detection
- Dependency security check
- Configuration file review
- Secret detection

#### Phase 3: Risk Prioritization
- CVSS scoring
- Exploitability assessment
- Impact analysis
- Remediation complexity

### Output Format
```markdown
# Security Audit Report

## Executive Summary
Overall security posture and critical findings

## Critical Vulnerabilities
### Issue 1: [Vulnerability Name]
**Severity:** Critical/High/Medium/Low
**Location:** file:line
**Description:** Detailed explanation
**Impact:** Potential consequences
**Remediation:** Specific fix steps
```code
// Example vulnerable code
// Example secure code
```

## Recommendations
Prioritized security improvements

## Compliance Status
Standards adherence checklist
```

### Triggering Examples
- "Perform security audit"
- "Check for vulnerabilities"
- "Review authentication security"
- "Scan for exposed secrets"

---

## Agent 6: Performance Optimizer

### Configuration
```yaml
name: performance-optimizer
model: opus
color: yellow
tools: Glob, Grep, LS, Read, NotebookRead, Bash, TodoWrite, WebSearch
```

### Purpose
Analyzes code performance, identifies bottlenecks, and provides optimization recommendations for algorithms, database queries, and system resources.

### Core Capabilities

1. **Performance Analysis**
   - Algorithm complexity evaluation
   - Database query optimization
   - Memory usage patterns
   - CPU utilization analysis
   - I/O operation efficiency
   - Network request optimization

2. **Bottleneck Detection**
   - N+1 query problems
   - Inefficient loops
   - Memory leaks
   - Blocking operations
   - Cache misses
   - Redundant computations

3. **Optimization Strategies**
   - Caching implementation
   - Query optimization
   - Algorithm improvements
   - Lazy loading
   - Connection pooling
   - Parallel processing

### Analysis Methodology

#### Phase 1: Profiling
- Identify hot paths
- Measure execution times
- Analyze resource usage
- Detect performance patterns

#### Phase 2: Bottleneck Analysis
- Pinpoint slow operations
- Evaluate algorithmic complexity
- Check database interactions
- Review network calls

#### Phase 3: Optimization Planning
- Prioritize improvements by impact
- Estimate implementation effort
- Consider trade-offs
- Plan incremental changes

### Output Format
```markdown
# Performance Analysis Report

## Performance Overview
Current performance metrics and issues

## Critical Bottlenecks
### Issue 1: [Performance Issue]
**Location:** file:line
**Current Performance:** O(n²) / 500ms
**Expected Performance:** O(n log n) / 50ms
**Impact:** User-facing latency

### Optimization:
```code
// Current implementation
// Optimized implementation
```
**Performance Gain:** 10x improvement

## Optimization Roadmap
1. Quick wins (< 1 day)
2. Medium-term improvements (1 week)
3. Long-term refactoring (> 1 week)
```

### Triggering Examples
- "Optimize this algorithm"
- "Why is the application slow?"
- "Improve database performance"
- "Reduce memory usage"

---

## Agent 7: Test Generator

### Configuration
```yaml
name: test-generator
model: sonnet
color: purple
tools: Glob, Grep, LS, Read, NotebookRead, Write, Edit, MultiEdit, TodoWrite
```

### Purpose
Creates comprehensive test suites including unit tests, integration tests, and edge case coverage for existing code.

### Core Capabilities

1. **Test Types**
   - Unit tests for individual functions
   - Integration tests for components
   - Edge case testing
   - Error condition testing
   - Boundary value testing
   - Regression test creation

2. **Coverage Analysis**
   - Statement coverage
   - Branch coverage
   - Path coverage
   - Edge case identification
   - Missing test detection

3. **Test Quality Features**
   - Mock/stub generation
   - Test data factories
   - Assertion completeness
   - Test isolation
   - Deterministic testing
   - Performance test creation

### Test Generation Methodology

#### Phase 1: Code Analysis
- Understand function purpose
- Identify parameters and returns
- Map code paths
- Detect edge cases

#### Phase 2: Test Design
- Create test scenarios
- Design test data
- Plan mock requirements
- Structure test suites

#### Phase 3: Test Implementation
- Write comprehensive tests
- Include positive/negative cases
- Add edge case coverage
- Ensure test independence

### Output Format
```typescript
// Example for TypeScript/Jest
describe('ComponentName', () => {
  describe('methodName', () => {
    it('should handle normal case', () => {
      // Arrange
      const input = setupTestData();
      
      // Act
      const result = methodName(input);
      
      // Assert
      expect(result).toBe(expectedValue);
    });
    
    it('should handle edge case', () => {
      // Edge case testing
    });
    
    it('should handle error condition', () => {
      // Error testing
    });
  });
});
```

### Triggering Examples
- "Generate tests for this function"
- "Create unit tests"
- "Add test coverage"
- "Write integration tests"

---

## Agent 8: Software Engineer

### Configuration
```yaml
name: software-engineer
model: opus
color: purple
tools: Full tool access (all available tools)
```

### Purpose
Writes new code, fixes bugs, implements features, refactors existing code, and solves programming problems with expertise across multiple languages and frameworks.

### Core Capabilities

1. **Code Creation**
   - New feature implementation
   - Algorithm development
   - Data structure design
   - API endpoint creation
   - Module/class construction

2. **Bug Fixing**
   - Root cause analysis
   - Error resolution
   - Performance fixes
   - Logic corrections
   - Edge case handling

3. **Code Refactoring**
   - Pattern implementation
   - Structure improvement
   - Performance optimization
   - Code cleanup
   - Technical debt reduction

4. **Quality Standards**
   - SOLID principles
   - Design patterns
   - Error handling
   - Input validation
   - Security practices
   - Testing considerations

### Development Approach

#### For New Code:
1. Clarify requirements
2. Consider system context
3. Design integrated solution
4. Implement with edge cases
5. Add logging/debugging
6. Write self-documenting code

#### For Bug Fixes:
1. Analyze root cause
2. Understand intended behavior
3. Preserve functionality
4. Test multiple scenarios
5. Document fix rationale
6. Check for similar issues

### Technical Expertise
- OOP and functional paradigms
- Asynchronous programming
- Database design
- API design (REST/GraphQL)
- Security best practices
- Performance optimization
- Version control

### Output Protocol
1. Explain implementation approach
2. Highlight assumptions/trade-offs
3. Identify potential risks
4. Suggest testing strategies
5. Provide usage examples

### Triggering Examples
- "Implement a caching mechanism"
- "Fix this null reference exception"
- "Refactor using repository pattern"
- "Add authentication to this endpoint"
- "Optimize this algorithm"

---

## Agent Interaction Patterns

### Automatic Agent Chaining
Certain scenarios trigger automatic agent collaboration:

1. **Code Writing → Code Review**
   - After significant code creation, code-reviewer automatically reviews

2. **Code Changes → Documentation Update**
   - Major feature additions trigger documentation-specialist

3. **Security Concerns → Security Audit**
   - Authentication/authorization changes trigger security-auditor

4. **Performance Issues → Optimization**
   - Detected slowdowns trigger performance-optimizer

5. **New Code → Test Generation**
   - New functions/classes trigger test-generator

### Manual Agent Invocation
Users can explicitly request agents:
```
"Use the code-reviewer agent to review this implementation"
"Have the security-auditor check for vulnerabilities"
"Get the research-assistant to evaluate database options"
```

---

## Implementation Guide for Other LLM Systems

### Basic Requirements
1. **Task Routing System**: Ability to route requests to specialized agents
2. **Tool Integration**: Access to file system, search, and edit capabilities
3. **Stateless Execution**: Each agent invocation should be independent
4. **Configuration Format**: YAML or similar for agent definition

### Adaptation Steps

#### 1. Define Agent Format
```yaml
---
name: agent-identifier
description: |
  Detailed description of agent purpose
  Include triggering keywords and examples
tools: [list, of, available, tools]
model: model-selection
color: ui-color
---

# Agent Prompt
Detailed instructions for the agent's behavior
```

#### 2. Implement Router
- Keyword-based selection
- Context analysis for automatic selection
- Priority system for multiple matches

#### 3. Create Prompts
- Adapt to your LLM's instruction style
- Include clear role definition
- Specify output format requirements
- Add quality standards

#### 4. Integrate Tools
- Map to your system's capabilities
- Implement security boundaries
- Add error handling

#### 5. Add Triggers
- Keyword detection
- Context-based activation
- User-requested invocation

### Key Considerations

**Model Selection**
- Larger models (Opus) for complex tasks requiring deep reasoning
- Smaller models (Sonnet) for structured tasks with clear patterns

**Tool Security**
- Sandbox file system access
- Limit network requests
- Validate user permissions
- Audit tool usage

**Error Handling**
- Graceful degradation
- Fallback to general model
- Clear error messaging
- Retry mechanisms

**Performance**
- Cache agent configurations
- Parallel agent execution where possible
- Resource limits per agent
- Timeout handling

**User Experience**
- Clear agent activation indicators
- Progress updates for long tasks
- Ability to cancel/interrupt
- Result summarization

---

## Best Practices for Agent Development

### 1. Agent Design Principles
- **Single Responsibility**: Each agent should excel at one domain
- **Clear Boundaries**: Well-defined scope and capabilities
- **Composability**: Agents should work well together
- **Predictability**: Consistent output formats and behavior

### 2. Prompt Engineering
- **Role Definition**: Clear expertise boundaries
- **Structured Output**: Consistent formatting
- **Example-Driven**: Include examples in prompts
- **Error Guidance**: How to handle edge cases

### 3. Tool Selection
- **Minimal Set**: Only tools necessary for the task
- **Security First**: Least privilege principle
- **Performance**: Consider tool execution time
- **Reliability**: Prefer stable, well-tested tools

### 4. Testing Strategies
- **Unit Testing**: Test individual agent responses
- **Integration Testing**: Test agent interactions
- **Performance Testing**: Measure execution time
- **User Testing**: Validate usefulness

### 5. Documentation Standards
- **Clear Descriptions**: What the agent does
- **Usage Examples**: When to use the agent
- **Limitations**: What the agent cannot do
- **Dependencies**: Required tools and configurations

---

## Future Enhancements Roadmap

### Short-term (1-3 months)
1. **Enhanced Agent Discovery**
   - Better keyword matching
   - Context-aware selection
   - User preference learning

2. **Performance Metrics**
   - Execution time tracking
   - Success rate monitoring
   - User satisfaction metrics

3. **Agent Templates**
   - Pre-built agent configurations
   - Industry-specific agents
   - Custom agent wizard

### Medium-term (3-6 months)
1. **Agent Collaboration Protocol**
   - Inter-agent communication
   - Shared workspace
   - Task delegation

2. **Dynamic Tool Assignment**
   - Context-based tool access
   - Security-based restrictions
   - Performance optimization

3. **Agent Versioning**
   - A/B testing capabilities
   - Rollback mechanisms
   - Gradual rollouts

### Long-term (6-12 months)
1. **Agent Learning System**
   - Feedback-based improvement
   - Pattern recognition
   - Automated optimization

2. **Visual Agent Builder**
   - GUI for agent creation
   - Drag-and-drop tool selection
   - Visual prompt builder

3. **Agent Marketplace**
   - Community-contributed agents
   - Agent rating system
   - Automated quality checks

---

## Conclusion

This comprehensive documentation covers all 8 production-ready Claude Code agents, providing detailed specifications for their capabilities, methodologies, and use cases. The modular agent architecture enables specialized expertise while maintaining system coherence through standardized interfaces and execution models.

Each agent represents years of prompt engineering and refinement, optimized for specific domains while working harmoniously within the larger system. The suggested enhancements and implementation guide provide a clear path for evolution and adoption by other systems.

The agent system demonstrates the power of specialized AI assistants working in concert, each bringing domain expertise to complex software development challenges. This approach significantly enhances productivity while maintaining high quality standards across all aspects of the development lifecycle.

For implementers looking to adopt similar architectures, this documentation provides both the theoretical framework and practical details necessary for successful implementation, along with lessons learned and best practices developed through extensive real-world usage.