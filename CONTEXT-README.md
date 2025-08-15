# PRP (Product Requirement prompts)

A comprehensive library of assets and context engineering for Agentic Engineering, optimized for Claude Code. This repository provides the Product Requirement Prompt (PRP) methodology, pre-configured commands, and extensive documentation to enable AI-assisted development that delivers production-ready code on the first pass.

## What is PRP?

See [PRPs/README.md](PRPs/README.md) for the complete PRP concept documentation including:
- What is a PRP and how it differs from a PRD
- The three AI-critical layers (Context, Implementation Details, Validation Gates)
- Why context is non-negotiable

In short: A PRP is PRD + curated codebase intelligence + agent/runbook—the minimum viable packet an AI needs to ship production-ready code on the first pass.

## Getting Started

### Option 1: Clone and Start a New Project

1. **Clone this repository**:

2. **Create your project structure**:

   ```bash
   # Example for a TypeScript/Node.js project
   mkdir -p src tests
   touch src/index.ts
   touch package.json
   touch tsconfig.json
   npm init -y
   npm install typescript @types/node -D
   ```

## Using Claude Commands

The `.claude/commands/` directory contains 12 pre-configured commands that appear as slash commands in Claude Code.

### Available Commands

1. **PRP Creation & Execution**:
   - `/prp-base-create` - Generate comprehensive PRPs with research
   - `/prp-base-execute` - Execute PRPs against codebase
   - `/planning-create` - Create planning documents with diagrams
   - `/spec-create-adv` - Advanced specification creation
   - `/spec-execute` - Execute specifications

2. **Code Review & Refactoring**:
   - `/review-staged-unstaged` - Review git changes 
   - `/smart-commit` - Review git changes and provide commit

3. **Utilities**:
   - `/prime-core` - Prime Claude with project context
   - `/onboarding` - Onboarding process for new team members

### How to Use Commands

1. **In Claude Code**, type `/` to see available commands
2. **Select a command** and provide arguments when prompted
3. **Example usage**:
   ```
   /create-base-prp user authentication system with OAuth2
   ```

## Using PRPs

### Creating a PRP

1. **Use the template** as a starting point:

   ```bash
   cp PRPs/templates/prp_base.md PRPs/my-feature.md
   ```

2. **Fill in the sections**:
   - Goal: What needs to be built
   - Why: Business value and user impact
   - Context: Documentation, code examples, gotchas
   - Implementation Blueprint: Tasks and pseudocode
   - Validation Loop: Executable tests

3. **Or use Claude to generate one**:
   ```
   /create-base-prp implement user authentication with JWT tokens
   ```

### Executing a PRP

1. **Using Claude commands**:
   ```
   /execute-base-prp PRPs/my-feature.md
   ```

### PRP Best Practices

1. **Context is King**: Include ALL necessary documentation, examples, and caveats
2. **Validation Loops**: Provide executable tests/lints the AI can run and fix
3. **Information Dense**: Use keywords and patterns from the codebase
4. **Progressive Success**: Start simple, validate, then enhance

### Example PRP Structure

```markdown
## Goal

Implement user authentication with JWT tokens

## Why

- Enable secure user sessions
- Support API authentication
- Replace basic auth with industry standard

## What

JWT-based authentication system with login, logout, and token refresh

### Success Criteria

- [ ] Users can login with email/password
- [ ] JWT tokens expire after 24 hours
- [ ] Refresh tokens work correctly
- [ ] All endpoints properly secured

## All Needed Context

### Documentation & References

- url: https://jwt.io/introduction/
  why: JWT structure and best practices

- file: src/auth/basic_auth.ts
  why: Current auth pattern to replace

- doc: https://nodejs.org/en/learn/getting-started/nodejs-with-typescript
  section: Node.js with TypeScript setup

- doc: https://github.com/auth0/node-jsonwebtoken
  section: JWT implementation for Node.js

### Known Gotchas

// CRITICAL: Use RS256 algorithm for production

// CRITICAL: Store refresh tokens in httpOnly cookies

// CRITICAL: Implement token blacklist for logout

## Implementation Blueprint

[... detailed implementation plan ...]

## Validation Loop

### Level 1: Syntax & Style

npm run lint
npm run typecheck

### Level 2: Unit Tests

npm test -- auth.test.ts

### Level 3: Integration Test

curl -X POST http://localhost:3000/auth/login \
 -H "Content-Type: application/json" \
 -d '{"email": "test@example.com", "password": "testpass"}'
```

## Project Structure Recommendations

```
your-project/
|-- .claude/
|   |-- commands/          # Claude Code commands
|   `-- settings.json      # Tool permissions
|-- PRPs/
|   |-- templates/         # PRP templates
|   |-- ai_docs/          # Library documentation
|   |-- completed/        # Finished PRPs
|   `-- *.md              # Active PRPs
|-- CLAUDE.md             # Project-specific guidelines
|-- src/                  # Your TypeScript source code
|-- tests/                # Your test files
|-- dist/                 # Compiled JavaScript (gitignored)
`-- node_modules/         # Dependencies (gitignored)
```

## Setting Up CLAUDE.md

Create a `CLAUDE.md` file in your project root with:

1. **Core Principles**: KISS, YAGNI, etc.
2. **Code Structure**: File size limits, function length
3. **Architecture**: How your project is organized
4. **Testing**: Test patterns and requirements
5. **Style Conventions**: Language-specific guidelines
6. **Development Commands**: How to run tests, lint, etc.

See the example CLAUDE.md in this repository for a comprehensive template.

## Advanced Usage

### Running Multiple Claude Sessions

Use Git worktrees for parallel development:

```bash
git worktree add -b feature-auth ../project-auth
git worktree add -b feature-api ../project-api

# Run Claude in each worktree
cd ../project-auth && claude
cd ../project-api && claude
```


### Custom Commands

Create your own commands in `.claude/commands/`:

```markdown
# .claude/commands/my-command.md

# My Custom Command

Do something specific to my project.

## Arguments: $ARGUMENTS

[Your command implementation]
```

## Resources Included

### Documentation (PRPs/ai_docs/)

- `cc_base.md` - Core Claude Code documentation
- `cc_actions_sdk.md` - GitHub Actions and SDK integration
- `cc_best_practices.md` - Best practices guide
- `cc_settings.md` - Configuration and security
- `cc_tutorials.md` - Step-by-step tutorials

### Templates (PRPs/templates/)

- `prp_base.md` - Comprehensive PRP template with validation


---

Remember: The goal is one-pass implementation success through comprehensive context. Happy coding with Claude Code!
