# Code Map Specification - Language Neutral

## Overview
The Code Map (`/Docs/CodeMap.md`) provides a comprehensive, navigable overview of any codebase including file structure, modules/classes, functions/methods, properties, and architectural patterns. It serves as the single source of truth for understanding and navigating the project.

## Required Structure (In Order)

### 1. Header
```markdown
# [Project Name] Code Map

*Last Updated: YYYY-MM-DD HH:MM:SS*
```
**IMPORTANT**: The timestamp MUST be in exact format `YYYY-MM-DD HH:MM:SS` (24-hour format) to track precise update times.

### 2. Main Table of Contents
Must include line numbers for EVERY section to enable quick navigation:

```markdown
## Table of Contents

| Section | Line Number |
|---------|-------------|
| [Quick Navigation](#quick-navigation) | 20 |
| [Visual Architecture Overview](#visual-architecture-overview) | 50 |
| [Project Structure](#project-structure) | 120 |
| [Core Configuration Files](#core-configuration-files) | 180 |
| [Core Modules/Packages](#core-modules-packages) | 250 |
| [Services/Utilities](#services-utilities) | 400 |
| [Components/UI](#components-ui) | 600 |
| [Cross-File Dependencies](#cross-file-dependencies) | 900 |
| [Configuration Files](#configuration-files) | 980 |
| [Architecture Patterns](#architecture-patterns) | 1050 |
| [Development Guidelines](#development-guidelines) | 1120 |
| [Performance Considerations](#performance-considerations) | 1180 |
```

### 3. Quick Navigation Section
List primary entry points and key files:

```markdown
## Quick Navigation

### Primary Entry Points
- **Main Entry**: `path/to/main.ext:15` - Application initialization
- **Configuration**: `path/to/config.ext:12` - Core configuration
- **Routes/URLs**: `path/to/routes.ext:8` - Routing definitions
- **Database/Models**: `path/to/models.ext:24` - Data definitions

### Key Components
- **Authentication**: `path/to/auth.ext:20` - User authentication
- **Data Access**: `path/to/data.ext:18` - Data management
- **Business Logic**: `path/to/logic.ext:11` - Core algorithms
```

### 4. Visual Architecture Overview
ASCII diagram showing system architecture and component relationships:

```markdown
## Visual Architecture Overview

┌─────────────────────────────────────────────────────────┐
│                    Application Layer                      │
│                   Main Entry Point                        │
└─────────────────────────────────────────────────────────┘
                              │
        ┌─────────────────────┴─────────────────────┐
        ▼                                           ▼
┌──────────────────┐                    ┌──────────────────┐
│  Business Logic  │◄───────────────────►│   UI/Interface   │
│                  │                    │                  │
└──────────────────┘                    └──────────────────┘
        ▲                                           ▲
        └─────────────────────┬─────────────────────┘
                              ▼
                  ┌──────────────────┐
                  │   Data Layer     │
                  └──────────────────┘
```

### 5. Project Structure
Show directory tree with file counts and key files:

```markdown
## Project Structure

```
project-root/
├── src/                    # Source code
│   ├── core/              # Core functionality (15 files)
│   ├── ui/                # User interface (8 files)
│   ├── services/          # Business services (12 files)
│   ├── models/            # Data models (6 files)
│   └── utils/             # Utilities (10 files)
├── tests/                 # Test files
├── docs/                  # Documentation
└── config/               # Configuration files
```
```

### 6. Detailed Module Documentation

For EACH significant file, include:

#### File Header
```markdown
### [Module/Class Name]
**Path**: `full/path/to/file.ext` - [line count] lines
**Purpose**: [Brief description of the file's responsibility]
**Language**: [Programming language if relevant]
```

#### Section-Specific TOC (for files > 100 lines)
```markdown
#### Table of Contents
| Section | Line Number |
|---------|-------------|
| Imports/Includes | 1 |
| Constants/Config | 25 |
| Class/Module Definition | 45 |
| Public Functions | 78 |
| Private Functions | 234 |
| Helper Functions | 389 |
```

#### Complete Element Inventory

For **Object-Oriented Languages** (Classes/Objects):
```markdown
#### Properties/Fields
| Name | Line | Type | Access | Description |
|------|------|------|--------|-------------|
| userId | 15 | string/int | private | User identifier |
| isActive | 18 | boolean | public | Active status |

#### Methods
| Method | Line | Access | Returns | Async | Description |
|--------|------|--------|---------|-------|-------------|
| initialize() | 78 | public | void | Yes | Setup method |
| process() | 95 | public | Result | No | Main processing |
| validate() | 112 | private | boolean | No | Data validation |
```

For **Functional Languages** (Modules/Functions):
```markdown
#### Functions
| Function | Line | Exported | Returns | Pure | Description |
|----------|------|----------|---------|------|-------------|
| main | 12 | Yes | IO () | No | Entry point |
| calculate | 45 | Yes | Number | Yes | Core calculation |
| helper | 78 | No | String | Yes | Internal helper |

#### Types/Interfaces
| Type | Line | Kind | Description |
|------|------|------|-------------|
| User | 23 | Record | User data structure |
| Config | 34 | Type Alias | Configuration options |
```

For **Procedural Languages** (Functions/Procedures):
```markdown
#### Functions
| Function | Line | Scope | Returns | Description |
|----------|------|-------|---------|-------------|
| main() | 12 | global | int | Program entry |
| init_system() | 45 | global | void | System initialization |
| process_data() | 78 | static | Data* | Data processing |

#### Global Variables
| Variable | Line | Type | Scope | Description |
|----------|------|------|-------|-------------|
| config | 8 | Config | global | System configuration |
| state | 10 | State | global | Application state |
```

### 7. Cross-File Dependencies
Document module relationships and data flow:

```markdown
## Cross-File Dependencies

### Module Dependencies
#### [Module Name]
**Imports/Uses**:
- `ModuleA` - Data structures
- `ModuleB` - Utility functions

**Imported By**:
- `ModuleC` - Uses authentication
- `ModuleD` - Uses validation

### Data Flow
#### [Data/State Name]
**Producer**: `ModuleName` (`path/to/module:lineNumber`)
**Consumers**:
- `Module1` (`path:line`) - [Usage description]
- `Module2` (`path:line`) - [Usage description]
```

### 8. Configuration Files
List all configuration files with purposes:

```markdown
## Configuration Files

### Build/Package Configuration
- `package.json` / `pom.xml` / `Cargo.toml` - Dependencies
- `Makefile` / `build.gradle` - Build scripts
- `.env` / `config.yaml` - Environment settings

### Language-Specific Configuration
- [List relevant config files for the language]

### Development Configuration
- `.gitignore` - Version control exclusions
- `Dockerfile` - Container configuration
- CI/CD configuration files
```

### 9. Architecture Patterns
Document design patterns and architectural decisions:

```markdown
## Architecture Patterns

### Design Patterns Used
- **Pattern Name**: [Description]
  - Implementation: `path/to/implementation`
  - Purpose: [Why this pattern is used]

### Architectural Style
- **Style**: [e.g., MVC, Microservices, Event-Driven]
  - Rationale: [Why chosen]
  - Implementation details
```

### 10. Development Guidelines
Include guidelines for extending the codebase:

```markdown
## Development Guidelines

### Adding New Features
1. [Step-by-step process]
2. [Conventions to follow]

### Code Standards
- Naming conventions
- File organization
- Testing requirements
- Documentation standards
```

### 11. Performance Considerations
Document optimization strategies:

```markdown
## Performance Considerations

### Optimization Strategies
- [Strategy 1]: [Implementation details]
- [Strategy 2]: [Implementation details]

### Known Performance Issues
- [Issue]: [Mitigation approach]
```

## Language-Specific Extensions

For language-specific details, refer to supplementary files:
- **C#/.NET**: See `CLAUDE_CodeMap_CSharp.md`
- **Python**: See `CLAUDE_CodeMap_Python.md`
- **JavaScript/TypeScript**: See `CLAUDE_CodeMap_JavaScript.md`
- **Java**: See `CLAUDE_CodeMap_Java.md`
- **Go**: See `CLAUDE_CodeMap_Go.md`
- **Rust**: See `CLAUDE_CodeMap_Rust.md`

## Formatting Requirements

### Line Number References
- **ALWAYS** use format: `file_path:line_number`
- Include line numbers for EVERY section reference
- Show file sizes as line counts: `filename.ext - 450 lines`

### Tables
- Use consistent column headers across similar tables
- Adapt table columns to language paradigm (OOP vs Functional vs Procedural)
- Sort entries by line number for easy scanning

### Visual Elements
- Use box-drawing characters for ASCII diagrams: `┌ ─ ┐ │ └ ┘ ▼ ▲ ◄ ►`
- Maintain consistent diagram style throughout
- Keep diagrams readable in monospace fonts

### Navigation Features
- Multi-level TOCs: Main TOC + section-specific TOCs
- Every major section gets a line number in the main TOC
- Sections > 100 lines get their own internal TOC
- Quick Navigation section at the top for primary actions

## Quality Standards

### Completeness
- Document ALL public functions/methods
- Include ALL configuration files
- List ALL module dependencies
- Document ALL cross-file data flow

### Accuracy
- Verify all line numbers before finalizing
- Update immediately when files change significantly
- Remove references to deleted files
- Keep architectural diagrams current

### Readability
- Use clear, concise descriptions
- Group related items together
- Maintain consistent formatting
- Include whitespace for visual separation

## Update Process

When updating the code map:
1. Check the `Last Updated` date
2. Run version control log/diff to find changes since that date
3. Update line numbers for changed files
4. Add new files in appropriate sections
5. Remove deleted files
6. Update architectural diagrams if structure changed
7. Verify all cross-references still valid
8. Update the `Last Updated` date

## Examples

- **C#/.NET**: `/mnt/d/Documents/Code/GitHub/.Net/MeshForge/Docs/MeshForge-CodeMap.md`
- **Web/TypeScript**: `/mnt/d/Documents/Code/GitHub/Web/LelandGreenProductions/Docs/CodeMap.md`