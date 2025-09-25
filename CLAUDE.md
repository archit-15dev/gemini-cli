# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Gemini CLI is an open-source AI agent that brings the power of Gemini directly into your terminal. It's a TypeScript/Node.js project using React (via Ink) for the CLI interface, built with a monorepo structure using npm workspaces.

## Commands

### Development Commands

**Build and Development:**
- `npm run build` - Build the main project
- `npm run build:all` - Build main project, sandbox, and VSCode extension
- `npm run build:packages` - Build all workspace packages
- `npm run start` - Start the CLI application
- `npm run debug` - Start in debug mode with inspector

**Testing:**
- `npm test` - Run all tests in workspaces
- `npm run test:ci` - Run CI tests with coverage
- `npm run test:e2e` - Run end-to-end tests
- `npm run test:integration:all` - Run all integration tests (none, docker, podman)

**Code Quality:**
- `npm run lint` - Lint TypeScript files
- `npm run lint:fix` - Auto-fix lint issues
- `npm run typecheck` - Run TypeScript type checking
- `npm run format` - Format code with Prettier

**Complete Validation:**
- `npm run preflight` - Run full validation suite (clean, install, format, lint, build, typecheck, test)

### Single Test Execution

For testing individual packages or specific test files:
```bash
# Test a specific workspace
npm test --workspace @google/gemini-cli-core

# Test a specific file using vitest directly
npx vitest run path/to/test.file.ts
```

## Architecture

### Monorepo Structure

The project uses npm workspaces with the following key packages:

- **`packages/cli/`** - Main CLI interface using React/Ink for terminal UI
- **`packages/core/`** - Core business logic, tools, services, and API clients
- **`packages/a2a-server/`** - Agent-to-agent server functionality
- **`packages/test-utils/`** - Shared testing utilities
- **`packages/vscode-ide-companion/`** - VSCode integration

### Key Architecture Components

**Core System (`packages/core/src/`):**
- `core/` - Central client, chat management, content generation, and token handling
- `tools/` - Built-in tools (file operations, shell, web search, MCP integration)
- `services/` - File discovery, git operations, shell execution
- `config/` - Configuration management and settings
- `utils/` - Shared utilities (file operations, git, formatting, search)

**CLI Interface (`packages/cli/src/`):**
- `ui/` - React/Ink components for terminal interface
- `commands/` - Slash command implementations
- `config/` - CLI-specific configuration and argument parsing
- `services/` - CLI-specific services

**Tools and Extensions:**
- Built-in tools for file operations, shell commands, web search, and MCP (Model Context Protocol) servers
- Extensible architecture supporting custom tools and MCP server integration
- Support for various authentication methods (OAuth, API keys, Vertex AI)

### Key Design Patterns

- **TypeScript with strict typing** - Avoid `any`, prefer `unknown` with type narrowing
- **Functional programming** - Plain objects over classes, immutable patterns
- **ES Modules** - Use import/export for encapsulation instead of class privacy
- **React/Ink** - Functional components with hooks for CLI UI
- **Vitest** - Testing framework with comprehensive mocking patterns

The system is designed around a chat-based interaction model where users can execute commands, run tools, and interact with various AI models through a terminal interface.