# Mise Tasks Documentation

This document provides an overview of all available mise tasks in this project.

## Overview

This project uses [mise](https://mise.jdx.dev/) for task management and development tool versioning. Tasks are defined in `.mise.toml` and can also be created as standalone scripts in the `.mise/tasks/` directory.

## Task Rules

According to `.mise/task-rules.md`:

- All tasks must be encapsulated in a script (shell or python)
- All scripts must be placed in `./mise/tasks`
- All python scripts must be invoked using mise, e.g. `mise x -- python .mise/tasks/task.py`

## Available Tasks

### Example Tasks

These are example tasks included in the template. Customize or replace them based on your project needs:

#### `hello`

**Description:** Example hello world task

**Usage:**

```bash
mise run hello
```

**What it does:**
Prints a simple greeting message. This is a basic example to demonstrate how mise tasks work.

### Optional Tasks (Examples)

The following tasks are commented out in `.mise.toml` but can be uncommented and customized:

#### `build`

**Description:** Build the project

**Usage:**

```bash
mise run build
```

#### `test`

**Description:** Run tests

**Usage:**

```bash
mise run test
```

#### `dev`

**Description:** Start development server

**Usage:**

```bash
mise run dev
```

### File-based Tasks

File-based tasks are located in `.mise/tasks/` directory:

#### `review-pr` (Optional Git Workflow Task)

**Location:** `.mise/tasks/review-pr`
**Type:** Shell script
**Description:** Create a git worktree for reviewing a pull request

**Usage:**

```bash
mise run review-pr <pr_number> [--no-checkout]
```

**Parameters:**

- `<pr_number>` - The PR number to review
- `--no-checkout` - (Optional flag) Don't checkout the worktree after creation

**What it does:**
Creates a new git worktree in a directory named `../review-pr-<pr_number>` with a branch named `review/pr-<pr_number>`. This is useful for reviewing pull requests in isolation without affecting your main working directory.

**Note:** This task is specific to git-based projects with pull request workflows. Remove it if not needed for your project.

## Running Tasks

You can run tasks using any of these methods:

```bash
# Full command
mise run <task-name>

# Shorthand (if no conflict with mise commands)
mise <task-name>

# With arguments
mise run <task-name> arg1 arg2

# List all available tasks
mise tasks ls

# Show task dependencies
mise tasks deps

# Get task information
mise tasks info <task-name>
```

## Adding New Tasks

### Method 1: Manual TOML definition

Add to `.mise.toml`:

```toml
[tasks.your-task-name]
description = "Description of your task"
run = "your command here"
```

### Method 2: File-based task

1. Create an executable script in `.mise/tasks/`
2. Add a shebang line (e.g., `#!/usr/bin/env bash`)
3. Optionally add mise comments for configuration:

   ```bash
   #!/usr/bin/env bash
   #MISE description="Your task description"
   #MISE alias="shortcut"

   # Your script content here
   ```

## Task Configuration Options

Tasks support various configuration options:

- `description` - Human-readable description
- `alias` - Short alias for the task
- `depends` - Tasks that must run before this task
- `env` - Environment variables for the task
- `dir` - Directory to run the task from
- `sources` - Input files (for up-to-date checking)
- `outputs` - Output files (for up-to-date checking)
- `hide` - Hide from task listings
- `quiet` - Suppress mise output
- `raw` - Connect directly to stdin/stdout/stderr

## Examples

### Simple task

```toml
[tasks.hello]
description = "Say hello"
run = "echo 'Hello, World!'"
```

### Task with dependencies

```toml
[tasks.build]
description = "Build the project"
run = "npm run build"

[tasks.test]
description = "Run tests"
depends = ["build"]
run = "npm test"
```

### Task with environment variables

```toml
[tasks.dev]
description = "Start development server"
env = { NODE_ENV = "development" }
run = "npm run dev"
```

### Task with multiple commands

```toml
[tasks.setup]
description = "Setup the project"
run = [
  "npm install",
  "npm run build",
  "echo 'Setup complete!'"
]
```

## Common Project Task Patterns

Here are some common task patterns you might want to implement:

### Node.js/JavaScript Projects

```toml
[tasks.install]
description = "Install dependencies"
run = "npm install"

[tasks.build]
description = "Build the project"
run = "npm run build"

[tasks.test]
description = "Run tests"
run = "npm test"

[tasks.dev]
description = "Start development server"
run = "npm run dev"

[tasks.lint]
description = "Run linter"
run = "npm run lint"

[tasks.format]
description = "Format code"
run = "npm run format"
```

### Python Projects

```toml
[tasks.install]
description = "Install dependencies"
run = "pip install -r requirements.txt"

[tasks.test]
description = "Run tests"
run = "python -m pytest"

[tasks.lint]
description = "Run linter"
run = "python -m flake8"

[tasks.format]
description = "Format code"
run = "python -m black ."
```

### Docker Projects

```toml
[tasks.build]
description = "Build Docker image"
run = "docker build -t myapp ."

[tasks.run]
description = "Run Docker container"
run = "docker run -p 8080:8080 myapp"

[tasks.compose-up]
description = "Start services with docker-compose"
run = "docker-compose up -d"

[tasks.compose-down]
description = "Stop services with docker-compose"
run = "docker-compose down"
```

## Useful Commands

```bash
# List all tasks
mise tasks ls

# Show task dependencies as a tree
mise tasks deps

# Edit a task (creates file-based task if doesn't exist)
mise tasks edit <task-name>

# Run multiple tasks in parallel
mise run task1 ::: task2 ::: task3

# Run task with specific tools
mise run build --tool node@18

# Force run task (ignore up-to-date checks)
mise run build --force
```

## Customizing This Template

To customize this template for your project:

1. **Update `.mise.toml`:**
   - Uncomment and modify the example tasks
   - Add your project-specific tools in the `[tools]` section
   - Set up environment variables in the `[env]` section

2. **Add your tasks:**
   - Replace the example tasks with your actual build, test, and development commands
   - Add any project-specific tasks you need

3. **Update this documentation:**
   - Replace the example tasks with your actual tasks
   - Add documentation for any custom tasks you create
   - Remove sections that don't apply to your project

4. **Remove optional components:**
   - Delete the `review-pr` task if you don't need git worktree functionality
   - Remove any example tasks you don't need

## More Information

For more detailed information about mise tasks, see:

- [Mise Tasks Documentation](https://mise.jdx.dev/tasks/)
- [Task Configuration](https://mise.jdx.dev/tasks/task-configuration.html)
- [Running Tasks](https://mise.jdx.dev/tasks/running-tasks.html)