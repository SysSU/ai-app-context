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

- file: [exact/path/to/pattern/file.ts or .tsx]
  why: [Specific pattern to follow - service structure, error handling, component structure, hook usage, etc.]
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

```typescript
// TypeScript/Node.js Specific Gotchas:
// Example: Next.js 15 App Router - Route handlers must export named functions
// Example: 'use client' directive must be at top of file, affects entire component tree
// Example: Server Components can't use browser APIs or event handlers
// Example: TypeScript strict mode requires proper typing
// Example: Node.js ES modules require explicit file extensions in imports
// Example: Express.js middleware order matters for request processing
```

## Implementation Blueprint

### Data models and structure

Create the core data models, we ensure type safety and consistency.

```typescript
// TypeScript/Node.js Examples:
// - Zod schemas for validation
// - TypeScript interfaces/types
// - Database schema types (Prisma, TypeORM, etc.)
// - API response types
// - Component prop types
// - Service layer types
```

### Implementation Tasks (ordered by dependencies)

```yaml
# TypeScript/Node.js Examples:
Task 1: CREATE lib/types/{domain}.types.ts
  - IMPLEMENT: TypeScript interfaces and types for domain models
  - FOLLOW pattern: lib/types/existing.types.ts (interface structure, export patterns)
  - NAMING: PascalCase for interfaces, camelCase for properties
  - PLACEMENT: Type definitions in lib/types/

Task 2: CREATE lib/services/{domain}.service.ts
  - IMPLEMENT: {Domain}Service class with async methods
  - FOLLOW pattern: lib/services/database.service.ts (service structure, error handling)
  - NAMING: {Domain}Service class, async create*(), get*(), update*(), delete*() methods
  - DEPENDENCIES: Import types from Task 1
  - PLACEMENT: Service layer in lib/services/

Task 3: CREATE lib/validators/{domain}.validator.ts
  - IMPLEMENT: Zod schemas for request/response validation
  - FOLLOW pattern: lib/validators/existing.validator.ts (schema structure)
  - NAMING: {domain}RequestSchema, {domain}ResponseSchema
  - DEPENDENCIES: Import types from Task 1
  - PLACEMENT: Validation layer in lib/validators/

Task 4: CREATE app/api/{resource}/route.ts (Next.js) OR src/routes/{domain}.ts (Express)
  - IMPLEMENT: API endpoints calling service methods
  - FOLLOW pattern: app/api/existing/route.ts (Next.js) or src/routes/existing.ts (Express)
  - NAMING: GET, POST, PUT, DELETE named exports (Next.js) or router.get/post/etc (Express)
  - DEPENDENCIES: Import service from Task 2, validators from Task 3
  - PLACEMENT: API layer following framework patterns

Task 5: CREATE __tests__/services/{domain}.service.test.ts
  - IMPLEMENT: Unit tests for all service methods (happy path, edge cases, error handling)
  - FOLLOW pattern: __tests__/services/existing.service.test.ts (Jest/Vitest patterns)
  - NAMING: describe('{Domain}Service') with nested it() blocks
  - COVERAGE: All public methods with positive and negative test cases
  - PLACEMENT: Tests in __tests__ directory

Task 6: CREATE __tests__/api/{resource}.test.ts
  - IMPLEMENT: API endpoint tests with supertest or similar
  - FOLLOW pattern: __tests__/api/existing.test.ts (API testing approach)
  - MOCK: External service dependencies using jest.mock or vi.mock
  - COVERAGE: Request validation, success responses, error handling
  - PLACEMENT: API tests in __tests__/api/
```

### Implementation Patterns & Key Details

```typescript
// Show critical patterns and gotchas - keep concise, focus on non-obvious details

// TypeScript Service method pattern
export class {Domain}Service {
  async {domain}Operation(request: {Domain}Request): Promise<{Domain}Response> {
    // PATTERN: Input validation first (follow lib/services/existing.service.ts)
    const validated = {domain}RequestSchema.parse(request);

    // GOTCHA: [Library-specific constraint or requirement]
    // PATTERN: Error handling approach (reference existing service pattern)
    // CRITICAL: [Non-obvious requirement or configuration detail]

    return { status: 'success', data: result };
  }
}

// TypeScript Component pattern
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

// Next.js API Route pattern
export async function POST(request: Request) {
  try {
    // PATTERN: Request validation and service delegation
    const body = await request.json();
    const validated = {domain}RequestSchema.parse(body);
    
    const result = await {domain}Service.{operation}(validated);
    return NextResponse.json(result);
  } catch (error) {
    // PATTERN: Consistent error handling across API routes
    return NextResponse.json({ error: 'Internal server error' }, { status: 500 });
  }
}
```

### Integration Points

```yaml
DATABASE:
  - migration: "Add column 'feature_enabled' to users table"
  - index: "CREATE INDEX idx_feature_lookup ON users(feature_id)"
  - schema: "Update Prisma schema or TypeORM entities"

CONFIG:
  - add to: .env.local or .env (TypeScript/Node.js)
  - pattern: "FEATURE_TIMEOUT=30" for server-side env vars
  - pattern: "NEXT_PUBLIC_* for client-side env vars" (Next.js)
  - validation: "Use zod or similar for env var validation"

ROUTES:
  - file structure: app/feature-name/page.tsx (Next.js App Router)
  - api routes: app/api/feature-name/route.ts (Next.js)
  - express routes: src/routes/feature-name.ts (Express.js)
  - pattern: "Export named functions GET, POST, PUT, DELETE" (Next.js)
```

## Validation Loop

### Level 1: Syntax & Style (Immediate Feedback)

```bash
# TypeScript/JavaScript/Node.js Projects:
# Run after each file creation - fix before proceeding
npm run lint                    # ESLint checks with TypeScript rules
npx tsc --noEmit               # TypeScript type checking (no JS output)
npm run format                 # Prettier formatting

# Project-wide validation
npm run lint:fix               # Auto-fix linting issues
npm run type-check             # Full TypeScript validation
npm run format:write           # Auto-format all files

# Alternative tooling (if using Bun, pnpm, or yarn)
bun run lint && bun run type-check
pnpm lint && pnpm type-check
yarn lint && yarn type-check

# Expected: Zero errors. If errors exist, READ output and fix before proceeding.
```

### Level 2: Unit Tests (Component Validation)

```bash
# TypeScript/JavaScript/Node.js Projects:
# Test each component/service as it's created
npm test -- __tests__/{domain}.test.ts
npm test -- __tests__/services/{domain}.service.test.ts
npm test -- __tests__/api/{resource}.test.ts

# Full test suite for affected areas
npm test -- __tests__/services/
npm test -- __tests__/components/
npm test -- __tests__/hooks/

# Coverage validation (if available)
npm test -- --coverage --watchAll=false
npm run test:coverage          # If separate coverage script

# Alternative test runners
vitest run __tests__/{domain}.test.ts    # If using Vitest
jest __tests__/{domain}.test.ts          # If using Jest directly
bun test __tests__/{domain}.test.ts      # If using Bun

# Expected: All tests pass. If failing, debug root cause and fix implementation.
# CRITICAL: Update existing tests when changing behavior or interfaces
# CRITICAL: Write new tests for all new functionality before marking tasks complete
```

### Level 3: Integration Testing (System Validation)

```bash
# TypeScript/Node.js/Next.js Projects:
# Development server validation
npm run dev &
sleep 5  # Allow server startup time

# Health check validation (if health endpoint exists)
curl -f http://localhost:3000/api/health || echo "Service health check failed"

# Page load validation (Next.js)
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

# Node.js server validation (Express/Fastify)
node dist/server.js &  # If compiled to dist/
npm start &            # If using npm start script
sleep 3                # Allow startup time

# Database validation (if database integration)
# PostgreSQL
psql $DATABASE_URL -c "SELECT 1;" || echo "Database connection failed"
# MySQL
mysql -h $DB_HOST -u $DB_USER -p$DB_PASSWORD -e "SELECT 1;" || echo "Database connection failed"
# MongoDB
mongosh $MONGODB_URL --eval "db.runCommand({ping: 1})" || echo "Database connection failed"

# Environment validation
node -e "console.log('Node version:', process.version)"
npm --version

# Expected: All integrations working, proper responses, no connection errors
```

### Level 4: Creative & Domain-Specific Validation

```bash
# TypeScript/Node.js/Next.js Specific Validation:

# Production build performance
npm run build && npm run analyze  # Bundle analyzer if available
npm run build:analyze             # Alternative bundle analysis

# Type safety validation
npx tsc --noEmit --strict        # Strict TypeScript checking
npx tsc --noEmit --project tsconfig.json  # Project-specific config

# Next.js specific checks
npm run lint:next                # Next.js linting rules if available
npx next lint                    # Next.js built-in linting

# Package vulnerability scanning
npm audit                        # Check for security vulnerabilities
npm audit fix                    # Auto-fix vulnerabilities
yarn audit                       # If using Yarn
pnpm audit                       # If using pnpm

# Performance Testing (if performance requirements)
ab -n 100 -c 10 http://localhost:3000/{endpoint}
wrk -t12 -c400 -d30s http://localhost:3000/{endpoint}

# Bundle size analysis
npx bundle-analyzer              # If using webpack-bundle-analyzer
npx @next/bundle-analyzer        # Next.js bundle analyzer

# API Documentation Validation (if API endpoints)
npx swagger-codegen validate -i openapi.json
npx @apidevtools/swagger-cli validate api-spec.yaml

# Docker validation (if containerized)
docker build -t app:test .
docker run --rm app:test npm test

# Custom Business Logic Validation
# [Add domain-specific validation commands here]
# Example: Custom health checks, integration tests, etc.

# Expected: All creative validations pass, performance meets requirements
```

## Final Validation Checklist

### Technical Validation

- [ ] All 4 validation levels completed successfully
- [ ] All tests pass: `npm test` or `yarn test` or `pnpm test`
- [ ] Test coverage maintained or improved for modified code areas
- [ ] New tests written for new functionality (components, services, API endpoints)
- [ ] Existing tests updated to reflect changes in behavior or interfaces
- [ ] No linting errors: `npm run lint` or `npx eslint .`
- [ ] No type errors: `npx tsc --noEmit` or `npm run type-check`
- [ ] No formatting issues: `npm run format:check` or `npx prettier --check .`
- [ ] Production build succeeds: `npm run build`

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
- [ ] README.md updated to reflect any new features, setup requirements, or architectural changes
- [ ] Test documentation updated if testing patterns or setup changed

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
