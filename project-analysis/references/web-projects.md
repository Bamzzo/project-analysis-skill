# Web and App Project Analysis

Use this reference for frontend, backend, full-stack, Electron, desktop webview, or API-service projects.

## Frontend Questions

- What framework is used?
- Where is the app root?
- How is routing handled?
- Where are API clients defined?
- Where is global state stored?
- How is authentication handled?
- How are environment variables loaded?
- What build/dev scripts exist?
- How are errors displayed to users?

## Backend Questions

- What framework is used?
- Where is the app/server created?
- Where are routes registered?
- What middleware is installed?
- Where is configuration loaded?
- Where are request/response schemas defined?
- Where is business logic?
- What external services are called?
- How are errors returned?
- How are logs written?

## Full-Stack Flow

Trace:

```text
User interaction
-> UI handler
-> API client
-> HTTP request
-> backend route
-> service/controller
-> database/external API
-> response
-> UI state update
```

## Environment and Runtime

Identify:

- Dev server ports
- Backend ports
- Proxy config
- CORS
- Build output directory
- Electron main/preload/renderer split when applicable
- Required local services
- Required environment variables

## Common Failure Modes

- Frontend points at wrong backend URL
- CORS blocks request
- Environment variables only available at build time
- Backend route prefix mismatch
- API response shape changed
- Authentication token missing
- Dev server and packaged app differ
- Native dependency incompatible with Node/Electron version
- Generated build files committed accidentally

## Verification

Recommended checks:

- Typecheck
- Unit tests
- Build
- Health endpoint
- Manual UI smoke test
- Browser console logs
- Network tab / request logs
- Backend logs

## Recommended Output Additions

For web/app projects, add:

1. Frontend Runtime
2. Backend Runtime
3. API Surface
4. Environment Variables
5. Frontend-to-Backend Flow
6. Build and Packaging
7. UI Verification Plan
