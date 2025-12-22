# Online Examination System (ASP.NET Web Forms)

## Overview and Purpose
The Online Examination System is a monolithic ASP.NET Web Forms application that enables educators to create and manage examinations and allows students to register, take exams (MCQ and theory), and view results. The system uses SQL Server for persistence and Bootstrap for styling. Administrative features include leaderboards, exam configuration, question management, and queues for theory answer evaluation.

This README serves as the primary Code Document and entry point to the detailed documentation under the docs/ directory.

- Documentation Index: docs/README.md

## Features
The application provides the following capabilities as implemented by the Web Forms pages:
- Authentication and registration via LoginPage.aspx and SignUpPage.aspx
- Student dashboard (Dashboard.aspx) with navigation to profile, leaderboard, and exam actions
- StartExam flow (StartExam.aspx) with course selection (filtered by semester) and checks for already-taken exams
- Multiple Choice exams (MCQExam.aspx) with timers and answer submission
- Theory exams (TheoryExam.aspx) with timers and free-text answers
- Results page (ExamResult.aspx) with scoring and profile updates
- Leaderboard pages (Leaderboard.aspx, AdminLeaderboard.aspx)
- Administrative panel (AdminPanel.aspx) for:
  - Creating and editing exams (SetExam.aspx, EditExam.aspx, EditMCQ.aspx, EditTheory.aspx, MCQSet.aspx, TheorySet.aspx)
  - Managing queues for theory answer evaluation (AdminCourseQueue.aspx, AdminQueue.aspx) and viewing answers (ShowAns.aspx)
- PDF result download placeholder (DownloadPdf.aspx)
- Styling via Bootstrap CSS (CSS/bootstrap.css)
- SQL Server persistence configured in Web.config connectionStrings

## Supported Platforms and Versions
- ASP.NET Web Forms targeting .NET Framework 4.8 (compilation target per OnlineExamSystem/Web.config)
- SQL Server or SQL Server Express
- Visual Studio (2019 or later recommended) with IIS Express
- Bootstrap (included as CSS/bootstrap.css within the project)

## Installation (Windows)
1) Prerequisites  
- Windows 10/11  
- Visual Studio with .NET Framework development workload (2019 or newer recommended)  
- SQL Server or SQL Server Express and SQL Server Management Studio (SSMS)

2) Database Setup  
- Open: database-script/Online-Examination-System-Databse-Script.sql  
- Execute the script in SQL Server to create the database schema and seed data (if provided).  
- Record the database name and server instance for connectionStrings.

3) Configure Connection Strings  
- File: OnlineExamSystem/Web.config  
- Update the <connectionStrings> entries:
  - dbconnection
  - OnlineExamConnectionString
- Example:
  <connectionStrings>
    <add name="dbconnection" connectionString="Data Source=.\SQLEXPRESS;Initial Catalog=OnlineExamDB;Integrated Security=True" providerName="System.Data.SqlClient" />
    <add name="OnlineExamConnectionString" connectionString="Data Source=.\SQLEXPRESS;Initial Catalog=OnlineExamDB;Integrated Security=True" providerName="System.Data.SqlClient" />
  </connectionStrings>

Notes:
- Web.Debug.config and Web.Release.config are provided for transform-based deployment. Adjust transforms if you create publish profiles.
- In Web.config, compilation targets .NET Framework 4.8 while httpRuntime targetFramework is 4.5.2; this configuration is supported for the project as-is.

4) Restore Packages  
- Open the solution in Visual Studio and allow NuGet to restore packages as needed.  
- The repository includes Microsoft.CodeDom.Providers.DotNetCompilerPlatform and Microsoft.Net.Compilers under packages/.

## Setup and Configuration
- Web.config:
  - Confirm <compilation debug="true" targetFramework="4.8" />
  - Confirm <httpRuntime targetFramework="4.5.2" />
  - Set connectionStrings as described above.
- Bootstrap:
  - CSS/bootstrap.css is bundled and referenced by pages. Replace or upgrade if desired.

## How to Run
- Run with Visual Studio (IIS Express):
  - Open Online-Examination-System-3411/OnlineExamSystem.sln
  - Set OnlineExamSystem as the startup project
  - Press F5 to launch with IIS Express; Visual Studio assigns a local port
- Deploy to IIS:
  - Publish from Visual Studio using a publish profile
  - Ensure the application pool targets .NET Framework 4.x
  - Grant the site/application appropriate database access
  - Configure production connectionStrings in Web.config or via transforms
- Port note:
  - Some meta documentation may reference port 3001 for previews. In local IIS Express, the port is auto-assigned unless you configure it.

## Basic Usage Examples
- Student sign-up and login:
  - Navigate to SignUpPage.aspx to create an account, then log in via LoginPage.aspx
- Starting an exam:
  - From Dashboard.aspx choose Start Exam to open StartExam.aspx, select a course/exam type (MCQ or Theory), and begin
- Taking an MCQ:
  - Use MCQExam.aspx to select answers within the allotted time and submit
- Taking a Theory exam:
  - Use TheoryExam.aspx to enter free-text responses within the timer and submit
- Viewing results and leaderboards:
  - Visit ExamResult.aspx for scores and Leaderboard.aspx for standings
- Admin workflows:
  - AdminPanel.aspx → SetExam.aspx to create an exam
  - EditExam.aspx → EditMCQ.aspx / EditTheory.aspx to modify questions
  - Use MCQSet.aspx and TheorySet.aspx to build question sets
  - Manage theory evaluation queues via AdminCourseQueue.aspx/AdminQueue.aspx and review answers on ShowAns.aspx

## License
This project is licensed under the MIT License. See LICENSE for full text and attribution.

## Documentation Links
Start with the documentation index:
- docs/README.md

Additional topic references:
- docs/Architecture.md
- docs/Configuration.md
- docs/Interfaces.md
- docs/ProjectStructure.md
- docs/InlineComments.md
- docs/DocstringsGuide.md
- docs/Contributing.md
