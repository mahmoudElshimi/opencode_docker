# AGENTS.md — Guidelines for Agentic Coding Agents

## Repository Overview

This repository packages the **opencode-ai** CLI tool as a Docker image. It contains no application source code — only a `Dockerfile`, `README.md`, and `LICENSE`.

## Build / Lint / Test Commands

| Command | Description |
|---|---|
| `docker build -t opencode .` | Build the Docker image |
| `docker run -it --rm -u $(id -u):$(id -g) -v "$(pwd):/workspace" opencode` | Run opencode interactively, mounting the current directory |

There are **no lint, test, or type-check commands** — this repo has no application code to test.

### Running a single test

Not applicable. No test framework is configured.

### Verifying the build

After modifying the Dockerfile, always verify the image builds successfully:

```bash
docker build -t opencode .
```

### Verifying the runtime

To confirm the container runs correctly after a build:

```bash
docker run -it --rm -u $(id -u):$(id -g) -v "$(pwd):/workspace" opencode --help
```

## Code Style Guidelines

### General

- **Language**: Dockerfile (Docker), Markdown (docs)
- **Dockerfile conventions**:
  - Use `node:22-slim` as the base image
  - Combine `apt-get update` and `apt-get install` in a single `RUN` layer
  - Clean up apt caches with `rm -rf /var/lib/apt/lists/*`
  - Use `--no-install-recommends` for apt packages
  - Use `--omit=dev --no-audit --no-fund` flags for `npm install -g`
  - Set `WORKDIR /workspace`
  - Use exec-form `ENTRYPOINT` (JSON array syntax)
  - Pin versions when adding system packages (e.g., `git=1:2.39.2-1+deb12u1`)
  - Use line continuations (`\`) for multi-line `RUN` commands
  - Place `RUN` instructions before `WORKDIR` and `ENTRYPOINT`
- **Markdown conventions**:
  - Use ATX-style headers (`#`, `##`, `###`)
  - Use fenced code blocks with language tags
  - Separate sections with `---` horizontal rules
  - Keep lines under 120 characters where practical

### Imports / Dependencies

- No application dependencies — only the global npm package `opencode-ai`
- System dependencies limited to `git` and `ca-certificates`
- Do not add system packages unless required for opencode-ai to function
- Do not add npm packages — opencode-ai is the sole npm dependency

### Formatting

- Dockerfile: 4-space indentation is not used; no indentation for Dockerfile instructions
- Markdown: 2-space indentation for nested lists
- No trailing whitespace in any file
- Files should end with a single newline

### Naming Conventions

- Docker image tag: `opencode` (lowercase, no prefix)
- npm global package: `opencode-ai`
- File names: lowercase with hyphens if needed (e.g., `docker-compose.yml`)
- Environment variables: UPPER_SNAKE_CASE if any are introduced

### Types

Not applicable. This repository contains no typed source code.

### Error Handling

- Docker build failures should be addressed by verifying base image availability and npm package existence
- No runtime error handling is needed — opencode-ai manages its own errors
- If adding shell commands in `RUN`, use `set -e` to fail on errors

## Cursor / Copilot Rules

No `.cursor/rules/`, `.cursorrules`, or `.github/copilot-instructions.md` files exist in this repository.

## Project Structure

```
.
├── Dockerfile        # Docker image definition for opencode-ai
├── README.md         # Usage instructions
└── LICENSE           # MIT/X license
```

## Key Dependencies

- **Base image**: `node:22-slim`
- **System packages**: `git`, `ca-certificates`
- **Global npm package**: `opencode-ai` (installed without dev dependencies)
