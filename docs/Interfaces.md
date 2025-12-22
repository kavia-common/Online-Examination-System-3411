# Interfaces and UI Pages

## Overview
This application is primarily UI-first using ASP.NET Web Forms. The following pages constitute the main user and admin flows. Where applicable, include form inputs, expected outputs, and error conditions. If you introduce WebMethods or HTTP handlers, use the provided template to document endpoints.

## User-Facing Pages

### Login (LoginPage.aspx)
- Purpose: Authenticate user as Student or Teacher/Admin.
- Inputs: Username, Password, Role (if applicable).
- Outputs: Redirect to Dashboard.aspx on success; validation error on failure.
- Errors: Invalid credentials; missing fields.

### Sign Up (SignUpPage.aspx)
- Purpose: Create a new user account; upload profile image.
- Inputs: Name, Username, Password/Confirm, Semester, Contact details, Image (optional).
- Outputs: Success message; redirect to LoginPage.aspx.
- Errors: Password mismatch; duplicate username; invalid image format.

### Dashboard (Dashboard.aspx)
- Purpose: Navigation hub for students.
- Actions: View Profile, Leaderboard, Start Exam, Logout.
- Notes: Requires session authentication.

### Start Exam (StartExam.aspx)
- Purpose: Select course and exam type to begin.
- Inputs: Course (filtered by semester), Exam Type (MCQ/Theory).
- Outputs: Navigation to MCQExam.aspx or TheoryExam.aspx.
- Errors: Attempt already taken; no available exams.

### MCQ Exam (MCQExam.aspx)
- Purpose: Render MCQ questions with timer and record answers.
- Inputs: Selected options for each question; navigation controls.
- Outputs: Submission to calculate score; redirect to ExamResult.aspx.
- Errors: Time expired; missing selection.

### Theory Exam (TheoryExam.aspx)
- Purpose: Display theory questions and capture free-form answers with timer.
- Inputs: Text answers; navigation controls.
- Outputs: Submission stores answers for evaluation; may redirect to a confirmation or ExamResult.aspx after marking.
- Errors: Time expired.

### Exam Result (ExamResult.aspx)
- Purpose: Show score and performance summary.
- Outputs: Score, per-question breakdown (if implemented).
- Admin Notes: May update user profile with marks and totals.

### Leaderboard (Leaderboard.aspx)
- Purpose: Display ranking and performance data.
- Outputs: Paginated or tabular standings.

## Administrative Pages

### Admin Panel (AdminPanel.aspx)
- Purpose: Navigation hub for administrative features.
- Actions: Profile, Leaderboard, Set Exam, Edit Exam, Logout.

### Set Exam (SetExam.aspx)
- Purpose: Create a new exam configuration.
- Actions: Define title, course, timing, number of questions.

### Edit Exam (EditExam.aspx)
- Purpose: Modify exam configuration and route to question editing.
- Actions: Edit MCQ (EditMCQ.aspx), Edit Theory (EditTheory.aspx).

### Question Set Pages
- MCQSet.aspx, EditMCQ.aspx
- TheorySet.aspx, EditTheory.aspx
- Purpose: Create and edit question banks.

### Queue and Evaluation
- AdminCourseQueue.aspx / AdminQueue.aspx: Manage theory answer evaluation queue.
- ShowAns.aspx: Review and score theory answers.

### Admin Leaderboard
- AdminLeaderboard.aspx: View performance across users.

## Download PDF (DownloadPdf.aspx)
- Purpose: Generate/serve exam results as PDF.
- Notes: Code-behind includes placeholder; implement PDF generation (e.g., Crystal Reports or third-party PDFs).

## Template for WebMethods/Handlers Documentation
When adding static or script-callable endpoints:

- Path: /PageName.aspx/MethodName (for [WebMethod] static methods)
- HTTP Method: POST (for WebMethod), GET/POST for handlers
- Inputs: JSON body schema or query parameters
- Outputs: JSON result or file content
- Errors: HTTP status codes and message structure

Example:
```
Endpoint: /Leaderboard.aspx/GetTop
Method: POST
Input: { "count": 10 }
Output: { "items": [ { "user":"...", "score": 95 } ] }
Errors: 400 invalid count, 500 internal error
```

## Notes
- For new pages, add a subsection here including purpose, inputs/outputs, and navigation paths.
- Keep this document in sync with the actual navigation implemented in code-behind (Response.Redirect/Server.Transfer paths).
