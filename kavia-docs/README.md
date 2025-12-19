# Online Examination System 3411 - Documentation Suite

## Overview
This documentation suite provides a forward-engineering view of the Online Examination System 3411. It is intended for business stakeholders, project managers, architects, and developers. The application is an ASP.NET Web Forms-based monolithic web application using SQL Server for persistence and Bootstrap for styling. It supports user registration and login, student dashboard, MCQ and theory exams with timers, administrative management of exams and questions, leaderboards, and exam results.

## Documents
- BRD: kavia-docs/requirements/BRD.md
- PRD: kavia-docs/requirements/PRD.md
- SRS: kavia-docs/requirements/SRS.md
- HLD: kavia-docs/design/HLD.md
- LLD: kavia-docs/design/LLD.md
- UML Diagrams: kavia-docs/design/UML.md
- Architecture: kavia-docs/architecture/ARCHITECTURE.md
- Project Planning: kavia-docs/planning/PROJECT-PLAN.md
- SDD / Technical Specification: kavia-docs/technical/SDD.md

## Technology Snapshot
- Frontend: ASP.NET Web Forms with Bootstrap CSS
- Backend: ASP.NET Web Forms code-behind (C# .NET Framework 4.8)
- Database: SQL Server (schema created from provided script)
- Hosting: IIS / ASP.NET Development Server
- Notable pages: LoginPage.aspx, SignUpPage.aspx, Dashboard.aspx, StartExam.aspx, MCQExam.aspx, TheoryExam.aspx, AdminPanel.aspx, AdminQueue/AdminCourseQueue.aspx, Leaderboard.aspx, ExamResult.aspx

## Source References
This suite was authored using the current repository content including:
- Web.config, OnlineExamSystem.csproj, representative code-behind files, and the SQL database script
- Top-level README and screenshots
