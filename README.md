# AI App Context Engineering Framework

A **TypeScript-focused PRP (Product Requirement Prompt) Framework** for context engineering with AI assistants, specifically optimized for Next.js and Node.js development.

## Overview

This framework provides a structured approach to creating comprehensive, executable prompts that enable AI assistants to successfully implement working code in a single pass. It emphasizes **context-first development** with built-in validation loops.

**Key Features:**
- 🎯 **PRP Templates** with validation-first design
- 🔧 **Pre-configured Claude Code commands** for rapid development
- 📚 **Curated AI documentation** for context injection
- ✅ **4-Level validation system** (syntax, tests, integration, domain-specific)
- 🏗️ **TypeScript/Node.js optimized** patterns and examples

## Quick Start

1. **Explore the Framework Structure:**
   ```bash
   tree -I 'node_modules|.git'
   ```

2. **Use Claude Code Commands:**
   - `/prp-base-create` - Generate comprehensive PRPs with research
   - `/prp-base-execute` - Execute PRPs against codebase
   - `/prime-core` - Prime Claude with project context

3. **Follow PRP Methodology:**
   - Start with `PRPs/templates/prp_base.md`
   - Include comprehensive context (documentation, examples, gotchas)
   - Define executable validation loops
   - Use TypeScript/Node.js patterns throughout

## Project Structure

```
ai-app-context/
├── .claude/
│   ├── commands/           # 28+ Claude Code commands
│   └── settings.local.json # Tool permissions
├── PRPs/
│   ├── templates/          # PRP templates with validation
│   ├── ai_docs/           # Curated Claude Code documentation
│   └── *.md               # Active and example PRPs
├── claude_md_files/        # Framework-specific CLAUDE.md examples
│   ├── CLAUDE-NEXTJS-15.md # Next.js 15 with React 19 guidelines
│   ├── CLAUDE-REACT.md     # React 19 development standards
│   └── CLAUDE-NODE.md      # Node.js 23 server-side guidelines
├── CLAUDE.md              # Project-specific Claude guidance
└── README.md              # This file
```

## Core Methodology

### PRP Best Practices

1. **Context is King** - Include ALL necessary documentation, examples, and caveats
2. **Validation Loops** - Provide executable tests/lints the AI can run and fix
3. **Information Dense** - Use keywords and patterns from the codebase
4. **Progressive Success** - Start simple, validate, then enhance

### 4-Level Validation System

```bash
# Level 1: Syntax & Style
npm run lint && npx tsc --noEmit

# Level 2: Unit Tests
npm test

# Level 3: Integration
npm run dev && curl -X POST http://localhost:3000/api/endpoint

# Level 4: Build & Deployment
npm run build
```

## Framework Principles

- **One-pass implementation success** through comprehensive context
- **Validation-first design** with executable checkpoints
- **TypeScript/Node.js optimization** for modern web development
- **Template-driven consistency** across all implementations
- **Anti-pattern awareness** to prevent common failures

## Getting Started

1. Read `CLAUDE.md` for project-specific guidance
2. Explore `PRPs/templates/prp_base.md` for the core template
3. Check `claude_md_files/` for framework-specific examples
4. Use `.claude/commands/` for rapid development workflows

## Contributing

When making changes to the framework:
- Follow existing PRP structure and validation patterns
- Update relevant documentation and examples
- Ensure all validation levels pass
- Update this README.md for significant changes

## Credits

Heavily inspired and based on [PRPs-agentic-eng](https://github.com/Wirasm/PRPs-agentic-eng) by Wirasm, adapted for TypeScript/Next.js development patterns.

---

**Remember:** This framework is about achieving **one-pass implementation success through comprehensive context and validation**. Every PRP should contain the exact context for an AI agent to successfully implement working code in a single pass.