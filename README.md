# CPF Project Template

This is a generic project template that uses [mise](https://mise.jdx.dev/) for task management and development tool versioning.

## Features

- **Task Management**: Pre-configured mise tasks for common development workflows
- **Tool Versioning**: Automatic tool version management with mise
- **Extensible**: Easy to customize for different project types
- **Documentation**: Comprehensive task documentation and examples

## Quick Start

1. **Clone or use this template**:
   ```bash
   # If using as a GitHub template
   gh repo create my-project --template your-username/cpf-project-template

   # Or clone directly
   git clone <this-repo-url> my-project
   cd my-project
   ```

2. **Install mise** (if not already installed):
   ```bash
   # macOS
   brew install mise

   # Linux
   curl https://mise.run | sh

   # Or see https://mise.jdx.dev/getting-started.html for other options
   ```

3. **Initialize the project**:
   ```bash
   # This will install any tools defined in .mise.toml
   mise install

   # Run the example task to verify everything works
   mise run hello
   ```

4. **Customize for your project**:
   - Edit `.mise.toml` to add your project's tools and tasks
   - Update `MISE_TASKS.md` with your actual task documentation
   - Remove or modify the example tasks as needed

## Project Structure

```
.
├── .mise/
│   ├── tasks/          # File-based tasks (shell scripts)
│   └── task-rules.md   # Task development guidelines
├── .mise.toml          # Mise configuration and task definitions
├── MISE_TASKS.md       # Task documentation
└── README.md           # This file
```

## Available Tasks

Run `mise tasks ls` to see all available tasks, or check `MISE_TASKS.md` for detailed documentation.

### Example Tasks

- `hello` - Example hello world task
- `review-pr` - Create git worktree for PR review (optional)

### Common Task Patterns (commented out in .mise.toml)

- `build` - Build the project
- `test` - Run tests
- `dev` - Start development server
- `lint` - Run linter
- `format` - Format code

## Customization Guide

### 1. Add Your Tools

Edit `.mise.toml` to specify the tools your project needs:

```toml
[tools]
node = "20"
python = "3.12"
terraform = "1.5.0"
```

### 2. Define Your Tasks

Replace the example tasks with your actual project tasks:

```toml
[tasks.build]
description = "Build the project"
run = "npm run build"

[tasks.test]
description = "Run tests"
depends = ["build"]
run = "npm test"
```

### 3. Set Environment Variables

Configure project-specific environment variables:

```toml
[env]
NODE_ENV = "development"
DATABASE_URL = "postgresql://localhost/myapp"
```

### 4. Update Documentation

- Modify this README.md for your project
- Update MISE_TASKS.md with your actual tasks
- Remove example content that doesn't apply

## Task Development Guidelines

See `.mise/task-rules.md` for guidelines on creating new tasks.

## Common Project Types

This template can be adapted for various project types:

### Node.js/JavaScript
- Uncomment and customize the Node.js tasks in `.mise.toml`
- Add tools like `node`, `npm`, or `pnpm`

### Python
- Add Python tools and virtual environment setup
- Use the Python task examples in `MISE_TASKS.md`

### Docker
- Add Docker-based tasks for building and running containers
- Use the Docker task examples in `MISE_TASKS.md`

### Multi-language
- Combine tools and tasks from different ecosystems
- Use mise's tool versioning to manage multiple language runtimes

## Contributing

1. Fork this repository
2. Create a feature branch
3. Make your changes
4. Update documentation
5. Submit a pull request

## License

[Add your license here]

## Resources

- [Mise Documentation](https://mise.jdx.dev/)
- [Mise Tasks Guide](https://mise.jdx.dev/tasks/)
- [Tool Configuration](https://mise.jdx.dev/configuration.html)
