# Online Examination System (ASP.NET Web Forms)

## Overview and Purpose
The Online Examination System is a classic ASP.NET Web Forms application that allows teachers to create and manage multiple-choice (MCQ) and theory exams, and enables students to register, take timed exams, view results, and track rankings on leaderboards. The system uses a traditional Master/Content layout with Bootstrap-based styling, server-side sessions for state management, and ADO.NET for database interactions via SQL Server.

This documentation provides a comprehensive guide for installing, configuring, and using the system, alongside details of platform support, features, and basic usage scenarios.

## Features
Based on the repository and in-app pages:
- User authentication for students and admin (teacher) with role-based navigation
- Admin panel to set up MCQ and theory exams for different courses, including editing existing questions and exams
- Student registration and the ability to start and complete timed MCQ/theory exams
- Leaderboard and exam result pages showing scores and rankings for completed exams
- Theory answer evaluation workflow with queues for pending scripts and a marking interface for teachers
- PDF download page (scaffolded in DownloadPdf.aspx, PDF generation code commented and ready to extend)

Limitations noted in repository README:
- In a single exam only five questions can be set (current implementation)
- The timer has known issues

## Repository Structure (high level)
- OnlineExamSystem.sln
- OnlineExamSystem/ (ASP.NET Web Forms project)
  - Web.config, Web.Debug.config, Web.Release.config
  - .aspx pages and code-behind (.aspx.cs), designer files (.aspx.designer.cs)
  - CSS/bootstrap.css
  - Properties/AssemblyInfo.cs
  - images and screenshots under top-level images/
  - packages.config
- database-script/
  - Online-Examination-System-Databse-Script.sql

For a detailed structure, refer to the Project Structure section in ARCHITECTURE.md.

## Installation

### Prerequisites
- Windows 10/11
- Visual Studio 2017 or later with:
  - ASP.NET and web development workload
  - .NET Framework 4.8 targeting pack
- IIS (recommended for deployment) or IIS Express (for local development)
- SQL Server (Developer or Express) and SQL Server Management Studio (SSMS)

### Steps
1. Clone the repository:
   - Use Git to clone or download the repository locally.
2. Open solution:
   - Open Online-Examination-System-3411/OnlineExamSystem.sln in Visual Studio.
3. Restore packages:
   - NuGet packages for CodeDom and Compilers are present in packages/.
   - Visual Studio should restore automatically; otherwise, run NuGet restore.
4. Configure database:
   - Create a SQL Server database.
   - Execute database-script/Online-Examination-System-Databse-Script.sql in SSMS to create the schema and seed as required.
5. Configure connection strings:
   - In OnlineExamSystem/Web.config, set:
     - connectionStrings/dbconnection
     - connectionStrings/OnlineExamConnectionString
   - Replace placeholder "your-database-connection-string" with a valid ADO.NET connection string:
     Example:
     Data Source=localhost;Initial Catalog=OnlineExamDb;Integrated Security=True;
6. Build:
   - Build the solution (Debug or Release).
7. Run:
   - Press F5 to run with IIS Express, or configure an IIS site pointing to OnlineExamSystem.

## Setup and Configuration
- Web.config key settings:
  - system.web/compilation: targetFramework="4.8"
  - system.web/httpRuntime: targetFramework="4.5.2"
  - connectionStrings:
    - dbconnection
    - OnlineExamConnectionString
- Packages:
  - Microsoft.CodeDom.Providers.DotNetCompilerPlatform (1.0.0)
  - Microsoft.Net.Compilers (1.0.0)
- Environment variables:
  - None defined in the repository. You may externalize database configuration via standard IIS/Web.config transforms or custom environment variables if desired.
- Web.config transforms:
  - Web.Debug.config and Web.Release.config included for environment-specific transforms.

## How to Run the Application
- Development (IIS Express):
  - Open the solution in Visual Studio and press F5. The application will start at an auto-assigned port.
- IIS:
  - Create a new site or application pointing to the OnlineExamSystem folder.
  - Ensure the app pool targets .NET Framework v4.0+ and Integrated pipeline.
  - Update connectionStrings in Web.config for the target environment.

## Basic Usage Examples (Navigating Main Pages)
- Login:
  - Navigate to LoginPage.aspx.
  - Student login: validated against userInfo table (via ADO.NET inline SQL).
  - Teacher login: current implementation accepts Admin/Admin for the admin panel.
- Student flows:
  - Dashboard.aspx: Navigate to StartExam.aspx to choose a course and exam type.
  - MCQExam.aspx: Timed MCQ exam with five questions; upon submission, redirects to ExamResult.aspx.
  - TheoryExam.aspx: Timed theory exam with question pairs; submission adds entries to theoryAns, queues in theoryCourseQueue and theoryQueue.
  - Leaderboard.aspx: View rankings for completed exams.
  - UserProfile.aspx: View basic profile details.
- Admin/Teacher flows:
  - AdminPanel.aspx: Access to SetExam.aspx, MCQSet.aspx, TheorySet.aspx to create questions/exams.
  - EditExam.aspx, EditMCQ.aspx, EditTheory.aspx: Modify previously created exams/questions.
  - AdminQueue.aspx/AdminCourseQueue.aspx: Review queues and navigate to ShowAns.aspx to evaluate theory answers.
  - AdminLeaderboard.aspx: Admin view of leaderboards.

## Supported Platforms and Versions
- .NET Framework: 4.8 (Project targets v4.8)
- ASP.NET: Web Forms
- Server: IIS/IIS Express
- Database: SQL Server

## License
- The repository includes a LICENSE file at the root. Review LICENSE for terms. If terms are unclear or missing details, treat as TBD until confirmed.

## Screenshots
Screenshots are available in images/ and referenced in the original project README.

## Notes on Security and Data Access
- Current code uses inline SQL string concatenation, which is vulnerable to SQL injection. Use parameterized queries for production deployments.
- Session-based access checks should be strengthened to avoid null references and unauthorized access.
- Timers are implemented server-side via a Timer control and session values; behavior and reliability should be validated.

## Troubleshooting
- If build reports missing compilers or providers, ensure packages are restored and Local Roslyn compilers are present under OnlineExamSystem/bin/roslyn.
- Confirm the database schema has been created and the connection string is correct.
- Verify App Pool identity has permissions to access the database if using SQL authentication or integrated security.

