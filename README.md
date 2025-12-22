# Online Examination System (ASP.NET Web Forms)

## Overview and Purpose
The Online Examination System is a monolithic ASP.NET Web Forms application that enables teachers to create and manage exams and allows students to register, take exams (MCQ and theory), and view results. It leverages SQL Server for persistence and Bootstrap for styling, offering administrative features such as leaderboards, exam configuration, question management, and queues for theory answer evaluation.

This README serves as the primary Code Document and entry point to the detailed documentation under the docs/ directory.

- Detailed docs index: see docs/ directory:
  - docs/InlineComments.md
  - docs/DocstringsGuide.md
  - docs/ProjectStructure.md
  - docs/Configuration.md
  - docs/Interfaces.md
  - docs/Contributing.md
  - docs/Architecture.md

## Features
The system includes the following features (as implemented in the project’s Web Forms pages):
- User authentication and registration via LoginPage.aspx and SignUpPage.aspx
- Student dashboard (Dashboard.aspx) showing navigation to profile, leaderboard, start exam, etc.
- StartExam flow (StartExam.aspx) with course selection filtered by semester and checks for taken exams
- Multiple Choice (MCQ) exams (MCQExam.aspx) with session-based timing and answer submission
- Theory exams (TheoryExam.aspx) with timers and typed answers
- Results page (ExamResult.aspx) with scoring and profile updates
- Leaderboard (Leaderboard.aspx) for viewing performance
- Admin panel (AdminPanel.aspx) for:
  - Creating/editing exams (SetExam.aspx, EditExam.aspx, EditMCQ.aspx, EditTheory.aspx, MCQSet.aspx, TheorySet.aspx)
  - Managing queues for theory answer evaluation (AdminCourseQueue.aspx/AdminQueue.aspx, ShowAns.aspx)
  - Viewing admin leaderboard (AdminLeaderboard.aspx)
- PDF download stub (DownloadPdf.aspx) for results (implementation placeholder in code-behind)
- Styling via Bootstrap CSS (CSS/bootstrap.css)
- SQL Server persistence via Web.config connectionStrings

## Supported Platforms and Versions
- ASP.NET Web Forms on .NET Framework 4.8
- SQL Server (SQL Server Express is acceptable)
- Visual Studio with IIS Express
- Bootstrap (version in repository: CSS/bootstrap.css; exact upstream version not specified)

## Installation (Windows)
1) Prerequisites
- Windows 10/11
- Visual Studio (recommended 2019 or later with .NET Framework development workload)
- SQL Server or SQL Server Express and SQL Server Management Studio (SSMS)

2) Database Setup
- Open the script at: database-script/Online-Examination-System-Databse-Script.sql
- Execute it in SQL Server to create the necessary database schema and seed data (if included).
- Note the resulting database name and server instance for use in connection strings.

3) Configure Connection Strings
- File: OnlineExamSystem/Web.config
- Update the values under <connectionStrings>:
  - dbconnection
  - OnlineExamConnectionString
- Example:
  <connectionStrings>
    <add name="dbconnection" connectionString="Data Source=.\SQLEXPRESS;Initial Catalog=OnlineExamDB;Integrated Security=True" providerName="System.Data.SqlClient" />
    <add name="OnlineExamConnectionString" connectionString="Data Source=.\SQLEXPRESS;Initial Catalog=OnlineExamDB;Integrated Security=True" providerName="System.Data.SqlClient" />
  </connectionStrings>

Note: Web.Debug.config and Web.Release.config are present for transform-based deployment. Ensure transforms are configured if you use publish profiles.

4) Restore Packages
- The project references Microsoft.CodeDom.Providers.DotNetCompilerPlatform and Microsoft.Net.Compilers via packages/ folder.
- If needed, open the solution in Visual Studio and allow NuGet to restore packages.

## Setup and Configuration
- Web.config:
  - Ensure <compilation debug="true" targetFramework="4.8" />
  - Ensure httpRuntime targetFramework is compatible (4.5.2 shown; compilation is 4.8).
  - Set connectionStrings as described above.
- Bootstrap reference:
  - CSS/bootstrap.css is included and referenced from pages. Update or replace as needed.

## Running the Application
- Visual Studio (IIS Express):
  - Open Online-Examination-System-3411/OnlineExamSystem.sln
  - Set OnlineExamSystem as the startup project (it is a Web Application)
  - Press F5 to run with IIS Express; Visual Studio will bind to a local port
- IIS Deployment Notes:
  - Publish from Visual Studio using a publish profile
  - Ensure application pool targets .NET Framework 4.x and that the site/application has required DB access
  - Configure connection strings via Web.config or Web.config transforms for Production

Note: The preview environment referenced in meta documentation uses port 3001; in local IIS Express, Visual Studio will auto-assign a port unless configured otherwise.

## Basic Usage
- Login:
  - Navigate to LoginPage.aspx and log in as Student or Teacher/Admin (create accounts via SignUpPage.aspx if needed)
- Start Exam:
  - From Dashboard.aspx, click Start Exam to open StartExam.aspx
  - Select course and exam type (MCQ or Theory) and begin
- MCQ Navigation:
  - MCQExam.aspx presents questions with options; submit answers within the timer
- Theory Navigation:
  - TheoryExam.aspx allows entering free-text answers; submit within the timer
- Admin Create/Edit Exam:
  - AdminPanel.aspx → SetExam.aspx to configure an exam
  - EditExam.aspx → EditMCQ.aspx / EditTheory.aspx to modify existing questions
  - Use MCQSet.aspx and TheorySet.aspx for creating question sets
- Results and Leaderboard:
  - ExamResult.aspx shows outcome; Leaderboard.aspx displays performance standings
  - Admins can view AdminLeaderboard.aspx

## License
- A LICENSE file exists in the repository. If the exact license terms need adjustment, consider MIT or another OSI license and update LICENSE accordingly.
- If no final decision is made, treat current LICENSE as authoritative and update this README after confirmation.

## Documentation Links
- Inline code comments guidance: docs/InlineComments.md
- C# XML doc comments standard: docs/DocstringsGuide.md
- Project structure overview: docs/ProjectStructure.md
- Configuration & environment: docs/Configuration.md
- UI pages and interfaces: docs/Interfaces.md
- Contributing & extension: docs/Contributing.md
- Architecture & flows: docs/Architecture.md
