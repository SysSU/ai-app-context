name: "Base PRP Template v3 - Implementation-Focused with Precision Standards"
description: |

---

## Goal

**Feature Goal**: [Specific, measurable end state of what needs to be built]

**Deliverable**: [Concrete artifact - API endpoint, service class, integration, React component, etc.]

**Success Definition**: [How you'll know this is complete and working]

## User Persona (if applicable)

**Target User**: [Specific user type - developer, end user, admin, etc.]

**Use Case**: [Primary scenario when this feature will be used]

**User Journey**: [Step-by-step flow of how user interacts with this feature]

**Pain Points Addressed**: [Specific user frustrations this feature solves]

## Why

- [Business value and user impact]
- [Integration with existing features]
- [Problems this solves and for whom]

## What

[User-visible behavior and technical requirements]

### Success Criteria

- [ ] [Specific measurable outcomes]

## All Needed Context

### Context Completeness Check

_Before writing this PRP, validate: "If someone knew nothing about this codebase, would they have everything needed to implement this successfully?"_

### Documentation & References

```yaml
# MUST READ - Include these in your context window
- url: [Complete URL with section anchor]
  why: [Specific methods/concepts needed for implementation]
  critical: [Key insights that prevent common implementation errors]

- file: [exact/path/to/pattern/file.py or .ts/.tsx]
  why: [Specific pattern to follow - class structure, error handling, component structure, hook usage, etc.]
  pattern: [Brief description of what pattern to extract]
  gotcha: [Known constraints or limitations to avoid]

- docfile: [PRPs/ai_docs/domain_specific.md]
  why: [Custom documentation for complex library/integration patterns, TypeScript/Next.js patterns]
  section: [Specific section if document is large]
```

### Current Codebase tree (run `tree` in the root of the project) to get an overview of the codebase

```bash

```

### Desired Codebase tree with files to be added and responsibility of file

```bash

```

### Known Gotchas of our codebase & Library Quirks

```python
# CRITICAL: [Library name] requires [specific setup]
# Example: FastAPI requires async functions for endpoints
# Example: This ORM doesn't support batch inserts over 1000 records
```

```typescript
// TypeScript/React Specific Gotchas:
// Example: Next.js 15 App Router - Route handlers must export named functions
// Example: 'use client' directive must be at top of file, affects entire component tree
// Example: Server Components can't use browser APIs or event handlers
// Example: TypeScript strict mode requires proper typing
```

## Implementation Blueprint

### Data models and structure

Create the core data models, we ensure type safety and consistency.

```python
Examples:
 - orm models
 - pydantic models
 - pydantic schemas
 - pydantic validators
```

```typescript
// TypeScript/JavaScript Examples:
// - Zod schemas for validation
// - TypeScript interfaces/types
// - Database schema types
// - API response types
// - Component prop types
```

### Implementation Tasks (ordered by dependencies)

```yaml
# Python Example:
Task 1: CREATE src/models/{domain}_models.py
  - IMPLEMENT: {SpecificModel}Request, {SpecificModel}Response Pydantic models
  - FOLLOW pattern: src/models/existing_model.py (field validation approach)
  - NAMING: CamelCase for classes, snake_case for fields
  - PLACEMENT: Domain-specific model file in src/models/

# TypeScript/JavaScript Example:
Task 1: CREATE lib/types/{domain}.types.ts
  - IMPLEMENT: TypeScript interfaces and types for domain models
  - FOLLOW pattern: lib/types/existing.types.ts (interface structure, export patterns)
  - NAMING: PascalCase for interfaces, camelCase for properties
  - PLACEMENT: Type definitions in lib/types/

Task 2: CREATE src/services/{domain}_service.py
  - IMPLEMENT: {Domain}Service class with async methods
  - FOLLOW pattern: src/services/database_service.py (service structure, error handling)
  - NAMING: {Domain}Service class, async def create_*, get_*, update_*, delete_* methods
  - DEPENDENCIES: Import models from Task 1
  - PLACEMENT: Service layer in src/services/

Task 3: CREATE src/tools/{action}_{resource}.py
  - IMPLEMENT: MCP tool wrapper calling service methods
  - FOLLOW pattern: src/tools/existing_tool.py (FastMCP tool structure)
  - NAMING: snake_case file name, descriptive tool function name
  - DEPENDENCIES: Import service from Task 2
  - PLACEMENT: Tool layer in src/tools/

Task 4: MODIFY src/main.py or src/server.py
  - INTEGRATE: Register new tool with MCP server
  - FIND pattern: existing tool registrations
  - ADD: Import and register new tool following existing pattern
  - PRESERVE: Existing tool registrations and server configuration

Task 5: CREATE src/services/tests/test_{domain}_service.py
  - IMPLEMENT: Unit tests for all service methods (happy path, edge cases, error handling)
  - FOLLOW pattern: src/services/tests/test_existing_service.py (fixture usage, assertion patterns)
  - NAMING: test_{method}_{scenario} function naming
  - COVERAGE: All public methods with positive and negative test cases
  - PLACEMENT: Tests alongside the code they test

Task 6: CREATE src/tools/tests/test_{action}_{resource}.py
  - IMPLEMENT: Unit tests for MCP tool functionality
  - FOLLOW pattern: src/tools/tests/test_existing_tool.py (MCP tool testing approach)
  - MOCK: External service dependencies
  - COVERAGE: Tool input validation, success responses, error handling
  - PLACEMENT: Tool tests in src/tools/tests/
```

### Implementation Patterns & Key Details

```python
# Show critical patterns and gotchas - keep concise, focus on non-obvious details

# Python Example: Service method pattern
async def {domain}_operation(self, request: {Domain}Request) -> {Domain}Response:
    # PATTERN: Input validation first (follow src/services/existing_service.py)
    validated = self.validate_request(request)

    # GOTCHA: [Library-specific constraint or requirement]
    # PATTERN: Error handling approach (reference existing service pattern)
    # CRITICAL: [Non-obvious requirement or configuration detail]

    return {Domain}Response(status="success", data=result)

# TypeScript Example: Component pattern
interface {Domain}Props {
  // PATTERN: Strict TypeScript interfaces (follow lib/types/existing.types.ts)
  data: {Domain}Data;
  onAction?: (id: string) => void;
}

export function {Domain}Component({ data, onAction }: {Domain}Props) {
  // PATTERN: Client/Server component patterns (check existing components)
  // GOTCHA: 'use client' needed for event handlers, useState, useEffect
  // CRITICAL: Server Components for data fetching, Client Components for interactivity

  return (
    // PATTERN: Consistent styling approach (see components/ui/)
    <div className="existing-class-pattern">
      {/* Follow existing component composition patterns */}
    </div>
  );
}

# Example: MCP tool pattern
@app.tool()
async def {tool_name}({parameters}) -> str:
    # PATTERN: Tool validation and service delegation (see src/tools/existing_tool.py)
    # RETURN: JSON string with standardized response format
```

### Integration Points

```yaml
DATABASE:
  - migration: "Add column 'feature_enabled' to users table"
  - index: "CREATE INDEX idx_feature_lookup ON users(feature_id)"

CONFIG:
  - add to: config/settings.py (Python) or .env.local (TypeScript/Next.js)
  - pattern: "FEATURE_TIMEOUT = int(os.getenv('FEATURE_TIMEOUT', '30'))" (Python)
  - pattern: "NEXT_PUBLIC_* for client-side env vars" (Next.js)

ROUTES:
  - add to: src/api/routes.py (Python)
  - pattern: "router.include_router(feature_router, prefix='/feature')" (Python)
  - file structure: app/feature-name/page.tsx (Next.js App Router)
  - api routes: app/api/feature-name/route.ts (Next.js)
```

## Validation Loop

### Level 1: Syntax & Style (Immediate Feedback)

```bash
# Python Projects:
# Run after each file creation - fix before proceeding
ruff check src/{new_files} --fix     # Auto-format and fix linting issues
mypy src/{new_files}                 # Type checking with specific files
ruff format src/{new_files}          # Ensure consistent formatting

# Project-wide validation
ruff check src/ --fix
mypy src/
ruff format src/

# TypeScript/JavaScript Projects:
# Run after each file creation - fix before proceeding
npm run lint                    # ESLint checks with TypeScript rules
npx tsc --noEmit               # TypeScript type checking (no JS output)
npm run format                 # Prettier formatting

# Project-wide validation
npm run lint:fix               # Auto-fix linting issues
npm run type-check             # Full TypeScript validation

# Expected: Zero errors. If errors exist, READ output and fix before proceeding.
```

### Level 2: Unit Tests (Component Validation)

```bash
# Python Projects:
# Test each component as it's created
uv run pytest src/services/tests/test_{domain}_service.py -v
uv run pytest src/tools/tests/test_{action}_{resource}.py -v

# Full test suite for affected areas
uv run pytest src/services/tests/ -v
uv run pytest src/tools/tests/ -v

# Coverage validation (if coverage tools available)
uv run pytest src/ --cov=src --cov-report=term-missing

# TypeScript/JavaScript Projects:
# Test each component/hook as it's created
npm test -- __tests__/{domain}.test.tsx
npm test -- __tests__/use{Hook}.test.ts

# Full test suite for affected areas
npm test -- components/{domain}/
npm test -- hooks/

# Coverage validation (if available)
npm test -- --coverage --watchAll=false

# Expected: All tests pass. If failing, debug root cause and fix implementation.
```

### Level 3: Integration Testing (System Validation)

```bash
# Python Projects:
# Service startup validation
uv run python main.py &
sleep 3  # Allow startup time

# Health check validation
curl -f http://localhost:8000/health || echo "Service health check failed"

# Feature-specific endpoint testing
curl -X POST http://localhost:8000/{your_endpoint} \
  -H "Content-Type: application/json" \
  -d '{"test": "data"}' \
  | jq .  # Pretty print JSON response

# TypeScript/Next.js Projects:
# Development server validation
npm run dev &
sleep 5  # Allow Next.js startup time

# Page load validation
curl -I http://localhost:3000/{feature-page}
# Expected: 200 OK response

# API endpoint validation
curl -X POST http://localhost:3000/api/{resource} \
  -H "Content-Type: application/json" \
  -d '{"test": "data"}' \
  | jq .  # Pretty print JSON response

# Production build validation
npm run build
# Expected: Successful build with no TypeScript errors or warnings

# MCP server validation (if MCP-based)
# Test MCP tool functionality
echo '{"method": "tools/call", "params": {"name": "{tool_name}", "arguments": {}}}' | \
  uv run python -m src.main

# Database validation (if database integration)
# Verify database schema, connections, migrations
psql $DATABASE_URL -c "SELECT 1;" || echo "Database connection failed"

# Expected: All integrations working, proper responses, no connection errors
```

### Level 4: Creative & Domain-Specific Validation

```bash
# MCP Server Validation Examples:

# Playwright MCP (for web interfaces)
playwright-mcp --url http://localhost:8000 --test-user-journey

# Docker MCP (for containerized services)
docker-mcp --build --test --cleanup

# Database MCP (for data operations)
database-mcp --validate-schema --test-queries --check-performance

# Custom Business Logic Validation
# [Add domain-specific validation commands here]

# TypeScript/Next.js Specific Validation:
# Production build performance
npm run build && npm run analyze  # Bundle analyzer if available

# Type safety validation
npx tsc --noEmit --strict        # Strict TypeScript checking

# Next.js specific checks
npm run lint:next                # Next.js linting rules if available

# Performance Testing (if performance requirements)
ab -n 100 -c 10 http://localhost:8000/{endpoint} # Python
ab -n 100 -c 10 http://localhost:3000/{endpoint} # TypeScript/Next.js

# Security Scanning (if security requirements)
bandit -r src/

# Load Testing (if scalability requirements)
# wrk -t12 -c400 -d30s http://localhost:8000/{endpoint}

# API Documentation Validation (if API endpoints)
# swagger-codegen validate -i openapi.json

# Expected: All creative validations pass, performance meets requirements
```

## Final Validation Checklist

### Technical Validation

- [ ] All 4 validation levels completed successfully
- [ ] All tests pass: `uv run pytest src/ -v` (Python) or `npm test` (TypeScript/JS)
- [ ] No linting errors: `uv run ruff check src/` (Python) or `npm run lint` (TypeScript/JS)
- [ ] No type errors: `uv run mypy src/` (Python) or `npx tsc --noEmit` (TypeScript)
- [ ] No formatting issues: `uv run ruff format src/ --check` (Python) or `npm run format --check` (TypeScript/JS)
- [ ] Production build succeeds: `npm run build` (TypeScript/Next.js projects)

### Feature Validation

- [ ] All success criteria from "What" section met
- [ ] Manual testing successful: [specific commands from Level 3]
- [ ] Error cases handled gracefully with proper error messages
- [ ] Integration points work as specified
- [ ] User persona requirements satisfied (if applicable)

### Code Quality Validation

- [ ] Follows existing codebase patterns and naming conventions
- [ ] File placement matches desired codebase tree structure
- [ ] Anti-patterns avoided (check against Anti-Patterns section)
- [ ] Dependencies properly managed and imported
- [ ] Configuration changes properly integrated

### TypeScript/Next.js Specific (if applicable)

- [ ] Proper TypeScript interfaces and types defined
- [ ] Server/Client component patterns followed correctly
- [ ] 'use client' directives used appropriately
- [ ] API routes follow Next.js App Router patterns
- [ ] No hydration mismatches between server/client rendering

### Documentation & Deployment

- [ ] Code is self-documenting with clear variable/function names
- [ ] TypeScript types/props interfaces properly documented (if applicable)
- [ ] Logs are informative but not verbose
- [ ] Environment variables documented if new ones added

---

## Anti-Patterns to Avoid

- ❌ Don't create new patterns when existing ones work
- ❌ Don't skip validation because "it should work"
- ❌ Don't ignore failing tests - fix them
- ❌ Don't use sync functions in async context
- ❌ Don't hardcode values that should be config
- ❌ Don't catch all exceptions - be specific
- ❌ Don't use 'use client' unnecessarily - embrace Server Components (Next.js)
- ❌ Don't ignore TypeScript errors with @ts-ignore - fix the types properly
