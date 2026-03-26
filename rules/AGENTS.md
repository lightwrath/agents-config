# Agent Coding Conventions

### Naming Conventions

| Context | Convention | Examples |
|---------|-----------|----------|
| Local variables | `camelCase`, short and descriptive | `matchedRoles`, `organizationNumberExists`, `clearanceDataAccessForRegion` |
| Private fields | `_camelCase` with underscore prefix | `_patchDocument`, `_profile`, `_principle` |
| Methods / Functions | `PascalCase` (C#), `camelCase` (TS/JS) | `GetOrganizationRoles()`, `useAccess()`, `getForm()` |
| Classes / Components | `PascalCase` | `OrganizationRoleService`, `TransactionRow`, `ActiveVoucher` |
| Interfaces (TS) | `I` prefix | `ITransactionRowProps`, `IOrganisationInfo`, `IVoucher` |
| Type aliases (TS) | `T` prefix | `TNewTransfer`, `TAction`, `TAppConfig` |
| Constants | `UPPER_SNAKE_CASE` | `DATE_FORMAT`, `ACCESS_API_V1_URL`, `ERROR_ISE` |
| DTOs (C#) | `Dto` suffix | `OrganizationRoleQueryRequestDto`, `OnboardingRegisterOrganizationResponseDto` |
| Files (TS) | PascalCase for components, camelCase for utils/hooks | `TransactionRow.tsx`, `useAccess.ts`, `fileUtils.ts` |
| Test files | `.cy.ts` / `.cy.tsx` (Cypress), `.test.ts` (Vitest/Jest) | `ActiveVoucher.cy.ts`, `Access.test.ts` |
| Styled components | Descriptive name or `Styled` prefix | `Row`, `Cell`, `StyledContainer` |

### Error Handling Philosophy

- Always validate inputs early. Prefer throwing descriptive exceptions from the service layer rather than returning error objects.
- Use `try/catch` at boundary layers (controllers, route handlers, API call sites) — not deep in business logic.
- Error messages must include context about what failed: `"Reserved organization number could not be found"`, not `"Not found"`.
- In Express routes: every handler gets its own `try/catch` that logs the error and returns the appropriate status code.
- In C#: use `ValidationException` for input validation failures. Use generic `Exception` with inner exception for infrastructure failures.
- In React: use error state values or thrown errors — never silently swallow failures.

### Async Patterns

- Always use `async/await`. Never use raw `.then()` promise chains.
- In C#: always propagate `CancellationToken` through the entire call chain — controller to service to repository.
- In C#: use `await using` for disposable async resources (transactions, connections).
- In C#: do not use `ConfigureAwait` — rely on ASP.NET Core's default synchronization context.
- In TypeScript: use `Promise.all()` to parallelize independent async operations.

### Code Organization

- Controllers and route handlers must be thin. They handle authorization, call services, and return responses. Business logic belongs in services or domain models.
- Keep type/interface definitions in dedicated files or directories (`types/`, or colocated `*.types.ts`).
- Colocate tests with source files where possible (`.cy.ts` next to `.tsx`, test classes in the same project).
- Use barrel exports (`index.ts`) for module boundaries.

### Documentation Style

- Use XML docs (`<summary>`, `<example>`, `<remarks>`) on public C# DTOs and API-facing models.
- Use inline comments only to explain **why**, not **what**. The code should be self-documenting for the "what".
- Do not over-comment. If a block of code needs extensive comments, refactor it to be clearer instead.

---

## C# / .NET Conventions

### Variable Declarations
- Always use `var` for local variable declarations. Explicit types are almost never used for locals.

### Primary Constructors for DI
- Always use C# 12 primary constructors for dependency injection — never field assignment in constructor bodies.
- Register services with scoped lifetime.

### Controller Structure
- Every controller gets full Swagger decoration: `[ApiController]`, `[LogicalApiVersion]`, `[SwaggerTag]`, standard error response codes (401, 403, 404, 400, 500), `[Produces]`, `[Consumes]`.
- Each action method has `[HttpGet/Post/etc]`, `[SwaggerOperation]`, `[SwaggerResponse]`, `[Authorize(Policy = ...)]`.
- Use `nameof()` for route names: `Name = nameof(GetOrganizationRolesV1)`.
- Controllers use primary constructors for DI, extending a `ControllerBase`.

### Service & Repository Pattern
- Services define contracts via interfaces in a separate `Interface/` folder.
- Interface methods omit the `public` modifier (C# convention for interfaces).
- Services call repositories; repositories handle EF Core queries.
- Async method names: Do not append `Async` suffix, unless there is going to be both a sync and async method.

### LINQ
- Always use method syntax. Never use query syntax (`from x in y select z`).
- Build queries incrementally using `AsQueryable()` with conditional `.Where()`.
- Use `.Contains()` for SQL `IN` operations.
- Use `.AsNoTracking()` and `.IgnoreQueryFilters()` for read-only performance queries.
- Use `.Select()` for projection into DTOs.

### DTO Mapping
- Prefer manual mapping with `.Select()` or object initializers over AutoMapper when the mapping is straightforward.
- Use AutoMapper only when the existing codebase already uses it or when mappings are complex.

### Null Handling
- Use nullable reference types consistently: `string?`, `Guid?`, `User?`.
- Prefer `FirstOrDefault()` + explicit null check over `First()`.
- Use pattern matching for null and property checks.
- Use null-coalescing `??` for defaults.

### Guard Clauses

- Always use single-line guard clauses for early returns, throws, and simple validation — no braces or multi-line blocks.
- Never wrap a single-statement guard in braces.
- Keep controller action methods compact — group guard clauses tightly with a blank line separating them from the business logic that follows.

## TypeScript / React Conventions

### Component Patterns
- Always use functional components. Never class components for React.
- Type components with `FC<T>`, `ReactFCC<T>`, or plain function signatures.
- Always destructure props in the function signature — never use `props.something`.
- Remove `PropsWithChildren` when `children` is not actually used by the component.
- Use default exports for components, named exports for hooks and utilities.

### TypeScript Typing
- Prefix interfaces with `I`, type aliases with `T`.
- Prefer `Array<T>` over `T[]` and `ReadonlyArray<T>` for immutable parameters.
- Use `as const` assertions for constant arrays and derive union types from them.
- Use generics for reusable classes and hooks.
- Use standalone type guard functions.

### State Management
- Use React Context + custom hooks for app-level state — no Redux.
- Use TanStack Query (React Query) for all server state.
- Query key factory pattern for organized cache keys.
- Class-based domain models are acceptable when modelling complex stateful entities (e.g., `ActiveVoucher`, `Organisation`, `Access`).

### API Integration
- Create custom query hooks with naming convention `use[Entity]Query`.
- Separate the data-fetching function from the hook definition.

### Styling
- Use Emotion `styled` components. Define them **below the component**, at the bottom of the file.
- Follow logical CSS property ordering: layout > box model > visual > typography > misc.
- Prefer modern CSS syntax: `rgb(14 22 27 / 7%)` over `rgba(14, 22, 27, 0.07)`.
- Use inline `css` prop only for one-off styles.

### Custom Hooks
- Name: `use[Purpose]` — e.g., `useAccess`, `useNavigateTo`, `useAppConfig`.
- Navigation hooks should encapsulate route logic:

### Import Organization
Follow this order (no comment separators needed, just consistent grouping):
1. React / framework imports
2. External library imports (`@talenom/*`, `@tanstack/*`, `formik`, `yup`)
3. Internal shared imports
4. Local imports (models, hooks, types, components)
5. Relative imports (sibling files, utils)

### JSX Patterns
- Conditional rendering with `&&`:
- Early return pattern for complex conditional branches — avoid deeply nested ternaries.
- Null coalescing for defaults in JSX: `recipient={transaction.CounterPartyName ?? '-'}`.
- Always provide explicit keys in `.map()` rendering.

## Node.js / Express Conventions
### Route Structure
- Use `express.Router()` per route module, exported and mounted in a central `routes/index.ts`:
- No separate controller layer — route handlers delegate directly to models/resource modules.
- `index.ts` (entrypoint) handles only server bootstrap (HTTPS, port binding). App setup and middleware go in `routes/index.ts`.

### Middleware
- Authentication middleware is inline in the route index, not in a separate file.
- Middleware order: logging > authentication > pre-validation > route handlers.
- Every route handler has its own `try/catch`.

### Config
- Centralized `config.ts` module using `dotenv`.
- Use `??` (nullish coalescing) for defaults, not `||`.
- Boolean env vars: `process.env.SERVER_ENABLE_MOCKS === 'true' || false`.

### Logging
- Use structured log calls with object parameters:
- Log levels via enum: `ERROR`, `WARN`, `INFO`, `DEBUG`.
- Redact sensitive data (national IDs, tokens) before logging.
- Log failures must never crash the application — wrap the logger itself in try/catch.

### Zero-Dependency Philosophy

Personal tools use **zero runtime dependencies** where possible. Rely on:
- Built-in Node/Bun APIs (`node:fs/promises`, `Bun.spawn`)
- Web standard APIs (`crypto.randomUUID()`, `TextDecoder`, `structuredClone`, `fetch`)
- No CLI frameworks, no logging libraries, no utility libraries (lodash, etc.)

### Strict TypeScript Configuration

When configuring TypeScript personally, use stricter settings than typical:
- **Module-level singleton** for config:

### Immutability via structuredClone
Getters that expose internal state return deep clones to prevent external mutation:

### Event-Driven Architecture
Strong preference for **EventEmitter hub** patterns for inter-module communication. Multiple personal projects use a central event bus:
- Modules subscribe/unsubscribe dynamically for feature toggling.
- React integration via `CustomEvent` on `document.body` when bridging non-React engines with React components.

### Monorepo Layout
Personal full-stack projects use a `client/` + `server/` split without workspace tooling:
No Lerna, no npm workspaces — just two independent `package.json` files.

### Functional by Default
Uses functions and module closures as the primary unit of organisation. Classes are used only when:
- A framework requires them (e.g., Phaser scene hierarchy).
- Modelling stateful domain objects (e.g., `Queue`, `Config`).
- Providing a static utility namespace (e.g., `Controller`, `FileSystem`).
  Everything else is plain functions, arrow functions for callbacks, and `function` declarations for named top-level exports.