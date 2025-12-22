# Contributing and Extension Guidelines

## Overview
Thank you for contributing to the Online Examination System. This is an ASP.NET Web Forms application using .NET Framework 4.8 and SQL Server. The application follows a traditional multi-page pattern with code-behind files managing UI events and data access.

## Development Environment
- Visual Studio 2017+ with ASP.NET workload
- .NET Framework 4.8 targeting pack
- SQL Server (Developer/Express)
- IIS Express for local dev, IIS for deployment

## Branching and PR Workflow
1. Fork the repository and create a feature branch:
   - Branch naming: feature/<short-name>, fix/<short-name>, docs/<short-name>
2. Keep commits small and focused.
3. Add or update documentation in kavia-docs/ when changing behavior or adding features.
4. Ensure the solution builds locally and new pages compile.
5. Open a Pull Request to main; include:
   - Summary of changes
   - Screenshots if UI changed
   - Notes on DB schema changes (and updated SQL script)

## Coding Standards (ASP.NET Web Forms)
- Use parameterized queries for all SQL operations (avoid string concatenation).
- Validate all inputs both client-side (when applicable) and server-side.
- Use consistent naming: PascalCase for methods and classes, camelCase/local variables.
- Factor repeated logic into helper methods or a dedicated data access layer class in App_Code (if introduced).
- Always check Session variables for null before use to prevent NullReferenceException.
- Prefer Response.Redirect over Server.Transfer unless preserving server execution context is required.
- Keep business logic out of UI where feasible; consider basic layering:
  - Presentation (pages)
  - Business logic helpers
  - Data access helpers

## Static Analysis and Formatting
- Enable Code Analysis in Visual Studio (FxCop analyzers for .NET Framework).
- StyleCop or EditorConfig (if added) for code style consistency.
- Use ReSharper/Roslyn analyzers optionally for additional inspection.
- Consider integrating SonarQube or similar tools for larger teams.

## Adding a New Feature (Example: New Exam Type)
1. Design:
   - Define new pages for creation, participation, and evaluation.
   - Extend database schema (add tables if necessary).
2. Database:
   - Modify database-script/Online-Examination-System-Databse-Script.sql and include upgrade notes.
3. UI:
   - Add new .aspx pages with corresponding .aspx.cs code-behind.
   - Update navigation links in Dashboard/StartExam/AdminPanel pages.
4. Business Logic:
   - Implement server event handlers with clearly documented methods.
   - Add robust validation and timing logic if applicable.
5. Data Access:
   - Create helper methods (App_Code/Data) with parameterized queries.
6. Tests:
   - Manual test plan and screenshots.
7. Documentation:
   - Update README and ARCHITECTURE with new flows and diagrams.
   - Add workflow entries in WORKFLOWS.md.
8. Security:
   - Ensure roles/authorization guard new pages.
   - Avoid exposing sensitive data in query strings.

## Making Database Changes
- Add SQL changes to the script and include comments explaining the migration.
- Consider versioning the script or providing incremental migrations in a scripts/ folder.
- Document impact on existing pages.

## Performance and Reliability
- Reduce repeated DB open/close by reusing connections within a using block.
- Cache reference data where appropriate (e.g., course names).
- Guard against time drift for timers; consider server-authoritative timing.

## Testing
- Manual scenarios:
  - Login (student/admin), exam start/submit, result view, leaderboard, admin question setup, theory evaluation.
- Data validation:
  - Empty inputs, boundary conditions, invalid course IDs.
- Security:
  - Unauthorized access attempts to admin pages.
  - Session expiration handling.

## Submitting a PR Checklist
- [ ] Builds successfully in Visual Studio
- [ ] Connection strings configurable; no secrets committed
- [ ] SQL changes updated and documented
- [ ] Pages have XML doc summaries and essential inline comments
- [ ] Updated documentation in kavia-docs/
- [ ] Screenshots attached if UI changes

