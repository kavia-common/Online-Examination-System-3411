# Business Workflows and Traceability

## Workflow Templates and Descriptions

### 1. Student Registration & Enrollment
- Actors: Student
- Trigger: Student selects “Sign Up” from Login page
- Preconditions:
  - Application running; database online
  - Student has required registration data
- Steps:
  1. Student opens LoginPage.aspx and clicks Sign Up.
  2. System transfers to SignUpPage.aspx.
  3. Student enters details and submits.
  4. System persists profile to userInfo and navigates to Login or Dashboard per flow.
- Postconditions:
  - New user record created.
- Business Value:
  - Opens access to exams and results.
- KPIs/Benefits:
  - Registration conversion rate, average time to register, error rate.

### 2. Exam Creation and Management (Admin)
- Actors: Admin/Teacher
- Trigger: Admin logs in and opens AdminPanel
- Preconditions:
  - Admin account or Admin/Admin credentials
- Steps:
  1. Admin navigates AdminPanel.aspx.
  2. Admin opens SetExam/MCQSet/TheorySet to create exams and questions.
  3. Admin uses EditExam/EditMCQ/EditTheory to modify existing content.
  4. Exam questions stored in mcqQS/theoryQS.
- Postconditions:
  - Exam and question records created/updated.
- Business Value:
  - Efficient preparation and updates for assessments.
- KPIs:
  - Number of exams created, edit frequency, time to publish.

### 3. Taking a Timed MCQ Exam
- Actors: Student
- Trigger: Student selects a course and MCQ exam
- Preconditions:
  - Student logged in; Session["_ID"] set
  - Course selected; Session["_Course"] set
- Steps:
  1. Student uses StartExam.aspx to select course/type.
  2. MCQExam.aspx loads five questions and initializes Session["Timer"].
  3. Student selects answers; on submit, system computes score.
  4. Result inserted into mcqTaken; redirects to ExamResult.aspx.
- Postconditions:
  - MCQ result stored; student sees score.
- Business Value:
  - Immediate, automated assessment.
- KPIs:
  - Average score, completion time, dropout rate.

### 4. Taking a Timed Theory Exam
- Actors: Student
- Trigger: Student selects a course and Theory exam
- Preconditions:
  - Student logged in; Session["_ID"] set
  - Course selected; Session["_Course"] set
- Steps:
  1. Student selects theory exam from StartExam.aspx.
  2. TheoryExam.aspx loads question pairs per sequence and sets timer.
  3. Student writes answers; on submission, five rows inserted into theoryAns.
  4. System enqueues in theoryCourseQueue and theoryQueue; inserts into theoryTaken.
  5. Transfers to Dashboard.
- Postconditions:
  - Theory answers persisted and queued for evaluation.
- Business Value:
  - Supports subjective assessment workflows.
- KPIs:
  - Queue length, average evaluation time, submission rate.

### 5. Theory Answer Evaluation (Teacher Queue & Marking)
- Actors: Teacher/Admin
- Trigger: New items in theoryQueue/theoryCourseQueue
- Preconditions:
  - Admin logged in
- Steps:
  1. Admin opens AdminQueue.aspx or AdminCourseQueue.aspx to view pending items.
  2. Select a course or student item to open ShowAns.aspx.
  3. Mark answers and approve results.
  4. Persist awarded marks and approvals (via ShowAns.aspx operations).
- Postconditions:
  - Evaluations recorded, status updated.
- Business Value:
  - Structured marking pipeline.
- KPIs:
  - Turnaround time, number of scripts evaluated per day, backlog size.

### 6. Leaderboard & Results Publication
- Actors: Student, Admin
- Trigger: Students complete exams; admin publishes results (implicit)
- Preconditions:
  - MCQ and evaluated theory results exist
- Steps:
  1. Students open Leaderboard.aspx to see rankings.
  2. Admin may use AdminLeaderboard.aspx to filter or review leaderboards.
- Postconditions:
  - Visibility of performance and rankings.
- Business Value:
  - Motivates learners, provides transparency.
- KPIs:
  - Participation rate, average rank gains, page engagement.

### 7. PDF Result/Summary Download
- Actors: Student, Admin
- Trigger: User opens DownloadPdf.aspx to export results
- Preconditions:
  - PDF generation integrated (currently scaffolded)
- Steps:
  1. User navigates to DownloadPdf.aspx.
  2. System would render a PDF from page content or result data (iTextSharp commented code exists).
  3. File downloads to the user’s device.
- Postconditions:
  - Offline copy of results.
- Business Value:
  - Portability, record-keeping.
- KPIs:
  - Number of PDFs downloaded, error rate, download time.

## Traceability: Pages to Business Processes
| Business Process                            | Pages/Modules                                                                 |
|--------------------------------------------|-------------------------------------------------------------------------------|
| User Authentication                         | LoginPage.aspx(.cs)                                                           |
| Student Registration                        | SignUpPage.aspx(.cs)                                                          |
| Dashboard & Navigation                      | Dashboard.aspx(.cs), StartExam.aspx(.cs), TakenCourses.aspx(.cs), UserProfile.aspx(.cs) |
| MCQ Exam Taking                             | MCQExam.aspx(.cs), ExamResult.aspx(.cs)                                       |
| Theory Exam Taking                          | TheoryExam.aspx(.cs)                                                          |
| Exam Setup (Admin)                          | AdminPanel.aspx(.cs), SetExam.aspx(.cs), MCQSet.aspx(.cs), TheorySet.aspx(.cs) |
| Edit Exams/Questions (Admin)                | EditExam.aspx(.cs), EditMCQ.aspx(.cs), EditTheory.aspx(.cs)                   |
| Theory Evaluation Queue & Marking (Admin)   | AdminQueue.aspx(.cs), AdminCourseQueue.aspx(.cs), ShowAns.aspx(.cs)           |
| Leaderboard/Results                         | Leaderboard.aspx(.cs), AdminLeaderboard.aspx(.cs)                              |
| PDF Export                                  | DownloadPdf.aspx(.cs)                                                          |

