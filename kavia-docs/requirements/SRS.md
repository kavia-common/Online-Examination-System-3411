# Software Requirements Specification (SRS)

## Introduction
This SRS specifies functional and non-functional requirements for the Online Examination System, aligned with the current ASP.NET Web Forms architecture and SQL Server schema.

## Functional Requirements
### User Management
- Register student accounts with profile image upload; persist in userInfo.
- Login with role selection (Student/Teacher); establish session and route accordingly.
- Logout from any page; clear session and redirect to login.

### Exam Management (Admin)
- Create/edit MCQ questions (MCQSet.aspx, EditMCQ.aspx) with options, correct answer, and tags.
- Create/edit Theory questions (TheorySet.aspx, EditTheory.aspx) with paired questions and marks.
- Set exams per course and semester (SetExam.aspx, EditExam.aspx).
- Manage queues for theory evaluation and course queues (AdminCourseQueue.aspx, AdminQueue.aspx).

### Student Exam Flows
- Course selection based on semester at StartExam.aspx.
- MCQ Exam:
  - Load five questions with options; show timer (eTime from mcqQS).
  - On submit, compute mark by comparing selected options to answers; insert row into mcqTaken.
  - Navigate to ExamResult.aspx.
- Theory Exam:
  - Load five question pairs (A/B) and marks; start timer (eTime from theoryQS).
  - On submit, insert answers into theoryAns; insert into theoryCourseQueue and theoryQueue; record in theoryTaken.

### Results and Leaderboards
- Display per-exam and cumulative results for students (ExamResult.aspx).
- Leaderboards by course/semester (Leaderboard.aspx).
- Optional PDF export (DownloadPdf.aspx; implementation placeholder present).

## Non-Functional Requirements
### Performance
- Page loads under typical intranet latency should render within 2 seconds for dashboard and navigation pages.
- Exam pages must update timers every second without causing full page reload; use UpdatePanel/Timer controls appropriately.
- Database operations for exam load/submit under 300 ms per query for typical dataset sizes.

### Security
- Use parameterized SQL commands to prevent SQL injection (currently concatenated; must be refactored).
- Secure session handling; always check session values safely and redirect if missing.
- Protect connection strings in Web.config; use least-privilege DB credentials.
- Restrict admin features to authorized users.

### Scalability
- Monolithic Web Forms app scaled vertically on IIS or horizontally with sticky sessions and a shared SQL Server.
- Database indexing on key tables (userInfo, mcqQS, theoryQS, mcqTaken, theoryTaken, theoryAns) to support read/write patterns.

### Usability
- Bootstrap-based responsive layout with clear navigation and accessible exam UI.
- Consistent timer visibility and exam progress feedback.

### Reliability and Availability
- Session-resilient exam pages with server-side timing authority to avoid client desync.
- Backup and restore plan for SQL Server; transaction integrity on submissions.

### Maintainability
- Separate concerns across pages and code-behind; centralize common DB access where feasible.
- Logging for errors and key actions to aid troubleshooting.

## Assumptions and Constraints
- .NET Framework 4.8 and ASP.NET Web Forms code-behind pattern.
- SQL Server is available and reachable with configured connectionStrings.
- Deployment on IIS with appropriate application pool settings.

## Data Model Overview
- userInfo: student profile and authentication data.
- mcqQS: MCQ question bank with options (op1-op4), ans, tag, eTime.
- theoryQS: Theory question bank with question pairs, marks, eTime.
- mcqTaken: MCQ submissions by student/course/exam with mark.
- theoryAns: Theory answers submitted per question; approval flags and marks.
- theoryTaken: Theory exam participation records.
- theoryQueue, theoryCourseQueue: Queues for evaluation workflows.

## Traceability Matrix (High-Level)
- Registration/Login -> userInfo, LoginPage.aspx.cs, SignUpPage.aspx.cs
- Start Exam -> StartExam.aspx.cs, mcqQS/theoryQS
- MCQ Exam -> MCQExam.aspx.cs, mcqQS, mcqTaken
- Theory Exam -> TheoryExam.aspx.cs, theoryQS, theoryAns, theoryQueue, theoryCourseQueue, theoryTaken
- Results/Leaderboard -> ExamResult.aspx.cs, Leaderboard.aspx.cs

## References
- Web.config, OnlineExamSystem.csproj, code-behind files for core flows, database script, project README.
