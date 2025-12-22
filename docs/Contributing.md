# Contributing and Extension Guidelines

## Workflow
- Create a feature branch from main.
- Keep commits small and focused.
- Open a Pull Request (PR) with a clear description, screenshots for UI changes, and manual test steps.
- Request review from maintainers.

## Coding Standards
- C# Style:
  - Use meaningful names, PascalCase for public members, camelCase for locals/parameters.
  - Prefer early returns to reduce nesting.
  - Handle exceptions explicitly; avoid swallowing exceptions.
- ASP.NET Web Forms:
  - Minimize code in Page_Load; factor logic into methods/services where possible.
  - Validate all user input server-side; encode outputs to prevent XSS.
  - Use parameterized SQL; avoid string concatenation for queries.
  - Manage session keys consistently (constants or helper).
  - Use ViewState thoughtfully; avoid large payloads.

## Adding New Features
1) New Page
- Add PageName.aspx with code-behind (.aspx.cs + .designer.cs).
- Add navigation from appropriate pages (e.g., Dashboard.aspx, AdminPanel.aspx).
- Include Bootstrap classes for consistent style.
- Update docs/Interfaces.md with the new page.

2) Data Model Changes
- Update the SQL script (create a new migration script if needed).
- Document schema changes in database-script/ and reference them in docs/Configuration.md.
- Update data access code accordingly.

3) Services/Repositories (Optional Refactor)
- Introduce Services/ and Repositories/ for separation of concerns.
- Add interfaces for testability.
- Document the new folders in docs/ProjectStructure.md.

## Submitting Changes
- Ensure solution builds in Visual Studio.
- Run manual tests for critical flows:
  - Login/Logout
  - Start and complete MCQ and Theory exams (with timer)
  - Admin create/edit questions
  - Leaderboard and results
- Lint/Format: Apply Visual Studio formatting; remove unused usings.
- Security review: validate/encode inputs, confirm parameterized SQL usage.

## Testing (Manual)
- Use seed data or create test users.
- Verify session timeouts and timer behavior.
- Confirm access control: students cannot access admin pages.

## Documentation
- Update README.md and docs/* when adding features or changing behavior.
- Include screenshots under images/ for UI updates.

## Release and Deployment
- Use Web.config transforms for environment differences.
- Verify connection strings and permissions in target IIS.
- Smoke-test after publish.

## License
- Follow LICENSE in repository. If changing license, discuss via PR and update README.md.
