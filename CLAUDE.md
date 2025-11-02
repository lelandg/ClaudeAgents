# USAGE: 1. Copy this file to ~/.claude/CLAUDE.md. 2. Restart all Claude instances.

## Work Procedures
- When I ask you to update the code map (or CodeMap), check the last date it was modified, then use git history to look for changes and update appropriate sections.
- When I ask you to review any code, always use the code reviewer agent.
- When I ask to update the code map, use the code map agent
- Use agent when one is available for a task.

### Code Review Agent Guidelines
**IMPORTANT**: When using the code-reviewer agent:
1. **Verify assumptions with actual code**: Don't assume issues exist - check the actual implementation
2. **Read files before claiming problems**: Always inspect the actual code rather than guessing based on patterns
3. **Check for existing implementations**: Many "potential" issues may already be properly handled
4. **Distinguish actual vs potential issues**: Focus on real problems, not theoretical ones
5. **Consider modern best practices**: Modern codebases often already implement proper patterns (IDisposable, async/await, etc.)

## Startup Procedures
- At startup, if ./CLAUDE.md exists and there is not a project-level `Docs/CodeMap.md` (e.g., `MeshForge/Docs/CodeMap.md` for the MeshForge project), offer to create it.

## Plan File Management

**CRITICAL**: Plan files in `Plans/` or `Notes/` directories must be kept current at all times to ensure continuity across sessions.

### When to Update Plan Files

Update the corresponding plan file **immediately** after:
1. **Completing any task or phase** - Mark with ✅ and status "COMPLETED"
2. **Starting a new task** - Mark with ⏳ and status "IN PROGRESS"
3. **Creating new files** - Document file paths and line counts
4. **Modifying existing files** - Note what was changed
5. **Discovering blockers** - Document issues and workarounds
6. **Changing approach** - Update strategy sections

### Required Updates

When updating plan files, you MUST:
1. **Mark task completion status**: Use ✅ (complete), ⏳ (in progress), ❌ (blocked), ⏸️ (paused)
2. **Add timestamps**: Update "Last Updated" at top of file or section
3. **Document deliverables**: List all files created/modified with line counts
4. **Update progress percentages**: Calculate phase completion (e.g., "Phase 2: 95% Complete")
5. **Add implementation notes**: Document deviations from plan, lessons learned
6. **Update "Status" sections**: Keep current status at top of each phase
7. **Cross-reference files**: Link to actual code files (e.g., `gui/video/ltx_controls_widget.py`)

### Plan File Format Standards

```markdown
## Phase N: [Phase Name] [Status Emoji] [Progress]

**Goal:** [Clear objective]

**Status:** Phase N is **[percentage]% complete**. [Current state summary]

**Last Updated:** YYYY-MM-DD HH:MM

### Tasks

1. ✅ Task description - **COMPLETED** (file.py:123)
   - Implementation details
   - Files created: `path/to/file.py` (N lines)
2. ⏳ Task description - **IN PROGRESS**
   - Current blocker or status
3. ❌ Task description - **BLOCKED**
   - Reason for blocking
4. Task description - **PENDING**

**Deliverables:** [Status Emoji]
- ✅ Deliverable 1 - Done
- ⏳ Deliverable 2 - In Progress
- Deliverable 3 - Pending
```

### Auto-Update Triggers

Automatically update the plan file when:
- Completing a TodoWrite task that's part of a plan
- Creating new files mentioned in the plan
- Finishing a phase or major milestone
- Encountering errors that affect the plan
- User asks to continue a plan (before starting work)

### Recovery After Interruption

When resuming after session interruption:
1. **Read the plan file first** - Check "Last Updated" and current status
2. **Review "Status" sections** - Understand what was in progress
3. **Check deliverables** - Verify which files were created
4. **Resume from last checkpoint** - Continue from last completed task
5. **Update plan immediately** - Mark current task as "IN PROGRESS"

### Example Update Workflow

```
# After completing a task:
1. Mark task ✅ in plan file
2. Update phase progress percentage
3. Add implementation notes
4. List files created/modified
5. Update "Last Updated" timestamp
6. Update "Status" section

# Before ending session:
1. Update all in-progress tasks with current state
2. Note any blockers or issues
3. Update "Status" section with next steps
4. Ensure timestamps are current
```

This ensures that even if power is lost or session ends abruptly, the plan file accurately reflects completed work and allows seamless resumption.

## Important Agent Usage Notes

**Agent File Creation**: When agents (documentation-specialist, code-reviewer, etc.) report creating files, always verify the file exists afterward. If it doesn't exist, create it directly using the Write tool with the agent's output. Agents sometimes indicate file creation in their summaries without the actual file being written due to their sandboxed execution environment.

**Agent Folder Documentation**: The file `Claude-Code-Agents-Documentation.md` in the `~/.claude/agents/` folder is documentation about agents, not an agent itself. When searching for or listing agents, ignore this file as it's reference documentation only.

### Code Navigation

#### Code Map Reference
**IMPORTANT**: Always use the comprehensive code map located at the project level `Docs/CodeMap.md` (e.g., `MeshForge/Docs/CodeMap.md` for the MeshForge project) for:
- **Finding classes and methods**: Detailed inventory with line numbers for quick navigation
- **Understanding file organization**: Complete project structure with cross-references
- **Locating shared variables**: Cross-file state management and variable usage
- **Navigating the codebase**: Organized by functional domains and architectural layers

**Code Map Currency Check**:
- **ALWAYS** check the last updated timestamp at the top of CodeMap.md before using it
- If the code map is older than 7 days, prompt: "The CodeMap.md was last updated on [YYYY-MM-DD HH:MM:SS]. Would you like me to update it first to ensure accuracy?"
- When updating code maps, the code-map-updater agent MUST include the exact timestamp in format: `*Last Updated: YYYY-MM-DD HH:MM:SS*`

The CodeMap.md contains:
- A table of contents with line numbers for each section
    - Then each section also has a table of contents with line numbers for each subsection
    - This allows you to quickly jump to specific parts of the codebase
- Complete file-by-file breakdowns of classes, methods, and properties with line numbers
- Architectural pattern documentation
- UI component mapping
- Configuration file locations

Use `file_path:line_number` references from the code map to quickly locate specific implementations.

## File Navigation Best Practices

**IMPORTANT**: Use the convenient symbolic links when working with MeshForge directories:

### MeshForge Symbolic Links (Project Root)
These symbolic links in the MeshForge project root provide quick access without long paths:
- **`_bin_debug`** → `/mnt/d/Documents/Code/GitHub/.Net/MeshForge/bin/Debug/net8.0-windows/win-x64`
- **`_bin_release`** → `/mnt/d/Documents/Code/GitHub/.Net/MeshForge/bin/Release/net8.0-windows/win-x64`
- **`_meshforge_appdata`** → `/mnt/c/Users/aboog/AppData/Roaming/MeshForge/` (logs, settings, licenses)
- **`_runtime_debug_files`** → `/mnt/d/Documents/Code/GitHub/.Net/MeshForge/bin/Release/net8.0-windows/win-x64/temp/`
- **`_screenshots`** → `/mnt/e/Pictures/Screenshots/2025`

### Working with Files Across Directories

#### Core Principles:
- **Never use `cd` commands**: Stay in the current working directory and use absolute paths
- **Always use full paths**: Specify complete paths like `/mnt/d/Documents/Code/GitHub/ProjectName/file.py`
- **Batch operations**: Call multiple tools in parallel when searching different locations

#### Tool-Specific Guidelines:

**For File Searches:**
- Use `Grep` with the `path` parameter: `Grep(pattern="TODO", path="/mnt/d/Documents/Code/GitHub/ProjectName")`
- Use `Glob` with the `path` parameter: `Glob(pattern="*.py", path="/mnt/d/Documents/Code/GitHub/ProjectName/src")`
- Combine patterns for efficiency: `Glob(pattern="**/*.{py,js,ts}", path="/absolute/path")`

**For File Operations:**
- Reading: Always provide full path: `Read(file_path="/mnt/d/Documents/Code/GitHub/ProjectName/src/main.py")`
- Listing: Use absolute paths: `LS(path="/mnt/d/Documents/Code/GitHub/ProjectName/src")`
- Editing: Full paths required: `Edit(file_path="/full/path/to/file.py", ...)`

**For Bash Commands:**
- Use absolute paths in commands: `python3 /mnt/d/Documents/Code/GitHub/ProjectName/script.py`
- For wildcards: `ls -la /mnt/d/Documents/Code/GitHub/*/README.md`
- For git operations: `git -C /mnt/d/Documents/Code/GitHub/ProjectName status`

## Development Environments
- I use Jetbrains IDEs. I have all products. I use PyCharm, Rider, and Webstorm a lot.
- **Python-specific Notes**
  - I have PyQt6 installed in Python for PowerShell, but not for bash (this shell). I will test it.
  - I have python3 for bash. I have Python 3.12 for PowerShell. I also have Anaconda, Docker, and other environments. I can test in one, if it will help.
- **.NET/C# Development Notes**
  - WPF applications require Windows to build and run fully
  - When working in WSL/Linux bash, use syntax checking instead of full builds
  - Check for compilation errors: `dotnet build --no-dependencies 2>&1 | grep -E "error CS|warning CS"`
  - Full builds (`dotnet build`) only work in PowerShell or Windows Command Prompt
  - Always verify syntax correctness before suggesting the user build in PowerShell

#### Efficiency Tips:
1. **Parallel searches**: When searching multiple directories, batch the tool calls in a single message
2. **Path variables**: When working repeatedly with a directory, note its absolute path at the start
3. **Avoid path traversal**: Use direct absolute paths instead of `../../../` constructions
4. **Git repository operations**: Use `git -C /absolute/path` to run git commands in other directories

#### Examples:
```bash
# Good - uses absolute path
Grep(pattern="class.*Controller", path="/mnt/d/Documents/Code/GitHub/MyProject")

# Bad - requires changing directory
cd /mnt/d/Documents/Code/GitHub/MyProject && grep -r "class.*Controller"

# Good - parallel operations with absolute paths
[
  Glob(pattern="*.md", path="/mnt/d/Documents/Code/GitHub/Project1"),
  Glob(pattern="*.md", path="/mnt/d/Documents/Code/GitHub/Project2")
]

# Good - git operation without changing directory
git -C /mnt/d/Documents/Code/GitHub/MyProject log --oneline -5
```

## Important Agent Usage Notes

**Agent File Creation**: When agents (documentation-specialist, code-reviewer, etc.) report creating files, always verify the file exists afterward. If it doesn't exist, create it directly using the Write tool with the agent's output. Agents sometimes indicate file creation in their summaries without the actual file being written due to their sandboxed execution environment.

## Documentation Procedures
- Any time you write to a CodeMap.md file, see ~/.claude/CLAUDE_CodeMap.md for specs.
- Any time I ask for documentation, use the documentation specialist agent.
- **Documentation Structure**:
  - Developer and user documentation goes in project-level `Docs/` directory (e.g., `MeshForge/Docs/` for the MeshForge project, not solution-level)
  - Future plans, ideas, and brainstorming go in project-level `Notes/` directory
  - Use markdown format (.md) as standard for all documentation
  - This allows separate documentation for main projects and test projects (e.g., `MeshForge/Docs/` vs `MeshForge.Tests/Docs/`)

## Credentials and Secrets Management

**CRITICAL**: Never store API keys, passwords, or credentials in project directories.

### Standard Pattern (ImageAI Model)

Store credentials in platform-specific user config directories **outside the project**:

- **Windows**: `%APPDATA%\Roaming\{AppName}\config.json`
- **macOS**: `~/Library/Application Support/{AppName}/config.json`
- **Linux**: `~/.config/{AppName}/config.json`

### Implementation Template

When creating configuration management for a new project:

1. **Create `config/user_config.py`** with `UserConfigManager` class:
   - `_get_config_dir()` - Returns platform-specific path
   - `load_config()` - Loads from user directory
   - `save_config()` - Saves to user directory
   - Include template generation function

2. **Update settings/config loading** to check user config as fallback:
   - Try environment variables first
   - Try project `.env` second (for non-secrets)
   - Fall back to user config directory for secrets

3. **Update `.gitignore`** to block common secret patterns:
   ```
   .env*
   !.env.example
   config.json
   secrets.json
   *.key
   *.pem
   *_credentials.json
   *_api_key.txt
   ```

4. **Create `config/README.md`** explaining:
   - Where config is stored
   - How to set it up
   - Configuration loading priority
   - Security notes

5. **Document in project CLAUDE.md** with:
   - User config location paths
   - Setup command (e.g., `python -m config.user_config`)
   - Configuration loading order

### Security Notes

- Project `.env` files can contain non-secret defaults, but **never** API keys
- User config directory is outside git - must be backed up separately
- Include encryption (like ImageAI's `secure_keys.py`) only when explicitly requested
- Always use absolute paths (`Path.home()`) to locate config
- Create config directory with `mkdir(parents=True, exist_ok=True)`

## Screenshots and Analysis Guidelines
- Screenshots are stored in `_screenshots` symlink (points to `/mnt/e/Pictures/Screenshots/2025`)
- To find the most recent screenshot, e.g., to find newest 3 use: `ls -lt _screenshots/*.png | head -3 | awk '{print $9}'`
- If I refer to just one "screenshot," look at the newest one based on timestamp.
- If I refer to "# screenshots," consider only the # newest. Examine the newest one first based on timestamp.
- Analyze and see if you can complete the task. Read the next older one only when needed.
- You can also use timestamps in the log to correlate screenshots with log entries.

## Node.js Version Management
- **Update Node.js to latest LTS**:
  - `nvm install --lts --reinstall-packages-from=default`
  - `nvm alias default lts/* && nvm use default`
- **Per-project version pinning**:
  - Create a `.nvmrc` in each repo (e.g., `lts/*` or `20`), then run `nvm use` in that directory
- I'm running server from PowerShell using .venv
- You're running in WSL. Use .venv_linux.
- Use python3 in WSL