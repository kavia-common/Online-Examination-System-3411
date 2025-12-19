# Product Requirements Document (PRD)

## Vision
Provide a reliable, accessible online platform where students can take MCQ and theory exams and receive results promptly, while educators efficiently create exams, manage questions, and evaluate theory answers.

## Target Users and Personas
### Student
- Needs: Simple registration/login, clear exam start/join flow, exam timer visibility, ability to view results and leaderboard.
- Motivations: Timely feedback, fairness, and usability.

### Teacher/Admin
- Needs: Create/edit exams, manage MCQ/theory questions, evaluate theory answers, publish results, monitor queues.
- Motivations: Efficiency, accuracy, and oversight.

## Key Product Features
- User Registration & Authentication (SignUpPage.aspx, LoginPage.aspx).
- Student Dashboard with course and exam listings (Dashboard.aspx, StartExam.aspx).
- MCQ Exams: Question rendering, option selection, timer, auto-marking (MCQExam.aspx).
- Theory Exams: Question rendering, answer submission, timer, queuing for evaluation (TheoryExam.aspx, ShowAns.aspx).
- Admin Capabilities: Create/edit exams and questions, manage queues (AdminPanel.aspx, MCQSet.aspx, TheorySet.aspx, EditMCQ.aspx, EditTheory.aspx, AdminCourseQueue.aspx, AdminQueue.aspx).
- Results & Leaderboards: Display results and rankings, export/download (ExamResult.aspx, Leaderboard.aspx, DownloadPdf.aspx).

## Non-Goals
- AI-based grading or proctoring.
- Offline exam support.
- Multi-tenant SaaS isolation.

## User Stories
- As a student, I can register and log in so I can take exams.
- As a student, I can view courses available for my semester and start an exam.
- As a student, I can take an MCQ exam with a visible timer and submit answers to see my mark.
- As a student, I can take a theory exam and submit answers that enter an evaluation queue.
- As an admin, I can create and edit MCQ and theory questions for specific courses and set exam parameters (e.g., time).
- As an admin, I can review theory answer queues and update marks/status.
- As an admin, I can view leaderboards and results and export them.

## Use Cases and Workflows
### Registration and Login
1. Student navigates to SignUpPage, submits details with uploaded image; data saved to userInfo.
2. Student navigates to LoginPage, authenticates; session is established and redirected to Dashboard.

### Start Exam
1. On StartExam.aspx, student’s semester determines available courses.
2. Student selects exam type (MCQ/Theory) and course.
3. System verifies course has available questions and navigates to respective exam page.

### MCQ Exam
1. Load five questions, options, and eTime (exam time).
2. Start timer based on eTime; on submit, calculate correct answers and insert record into mcqTaken.
3. Redirect to ExamResult.aspx.

### Theory Exam
1. Load five question pairs (A/B) with marks; start timer based on eTime.
2. On submit, insert answers into theoryAns; enqueue in theoryCourseQueue and theoryQueue.
3. Insert theoryTaken record; redirect with confirmation.

### Admin Queue Management
1. Admin views pending courses and student submissions in queue pages.
2. Admin evaluates, updates approvals, and publishes results.

## Acceptance Criteria
- Students can complete MCQ and theory exams with enforced timers.
- MCQ results computed and stored; theory answers stored and queued.
- Leaderboards reflect accurate rankings.
- Admins can create, edit, and manage questions and exams.

## Release Criteria
- Deployed on IIS with configured connectionStrings.
- All core flows validated in staging with sample data.

## Dependencies
- SQL Server database as defined in provided script.
- Bootstrap CSS for UI styling.

## Metrics
- Average time from exam completion to result availability.
- Number of exam sessions per day.
- Error rates in authentication and exam submission.

## Risks and Mitigations
- Timer reliability: Validate server-side time checks; avoid client-only timing.
- SQL injection via concatenated strings: Migrate to parameterized queries.
- Session handling: Validate sessions on every page load and handle null safely.

## References
- LoginPage.aspx.cs, SignUpPage.aspx.cs, StartExam.aspx.cs, MCQExam.aspx.cs, TheoryExam.aspx.cs, AdminCourseQueue.aspx.cs, AdminQueue.aspx.cs, ExamResult.aspx.cs, Leaderboard.aspx.cs, Web.config, database script, README.md.
