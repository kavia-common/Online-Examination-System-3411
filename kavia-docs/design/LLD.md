# Low-Level Design (LLD)

## Module Decomposition
### Authentication Module
- Pages: LoginPage.aspx(.cs)
- Responsibilities: Authenticate user against userInfo; set Session["_ID"]; route by role.
- Key Functions:
  - loginButton_Click: Validate credentials, set session, redirect.
- Data:
  - userInfo(id, password, name, department, semester, gender, email, etc.)

### Registration Module
- Pages: SignUpPage.aspx(.cs)
- Responsibilities: Capture student data, save image to ~/Images, insert into userInfo.
- Key Functions:
  - signUpB_Click: Validate passwords match, insert userInfo record.

### Course and Exam Selection Module
- Pages: Dashboard.aspx(.cs), StartExam.aspx(.cs)
- Responsibilities: Show courses based on semester; verify availability; set session data; navigate to exams.
- Key Functions:
  - Page_Load in StartExam: Load courses by semester; check mcqQS/theoryQS availability.
  - GridView1/2_SelectedIndexChanged: Start exam flow and route to TheoryExam.aspx/MCQExam.aspx.

### MCQ Exam Module
- Pages: MCQExam.aspx(.cs)
- Responsibilities: Load five MCQ questions, store expected answers in Session, handle timer, compute mark, insert into mcqTaken.
- Key Functions:
  - Page_Load: Multiple queries to mcqQS by course and question numbers 1..5; eTime read from qs 5.
  - submitB_Click: Compare selected answers to Session["_ansN"], compute mark, insert submission.

### Theory Exam Module
- Pages: TheoryExam.aspx(.cs)
- Responsibilities: Load five pairs of questions, manage timer, insert detailed answers into theoryAns, queue for evaluation, insert theoryTaken.
- Key Functions:
  - Page_Load: Sequentially load qsA/qsB and marks for qsNo from Session["_qNO"] onward.
  - submitB_Click: Insert answers, queue records, and taken record.

### Administration Module
- Pages: AdminPanel.aspx(.cs), MCQSet.aspx(.cs), TheorySet.aspx(.cs), EditMCQ.aspx(.cs), EditTheory.aspx(.cs), AdminQueue.aspx(.cs), AdminCourseQueue.aspx(.cs)
- Responsibilities: Author and modify questions/exams; manage evaluation queues; navigate to components.

### Results and Leaderboards
- Pages: ExamResult.aspx(.cs), Leaderboard.aspx(.cs), DownloadPdf.aspx(.cs)
- Responsibilities: Display results and rankings; optionally export PDFs (DownloadPdf has scaffolded code).

## Detailed Processing Logic (Representative)
### MCQExam: submitB_Click
- Read expected answers from Session["_ans1".." _ans5"].
- For each RadioButtonList1..5, increment mark if selected item text equals expected answer.
- Insert mcqTaken(studentID, courseID, examNo, mark).
- Redirect to ExamResult.aspx.

### TheoryExam: submitB_Click
- Read student and course from session.
- Insert five rows into theoryAns with question texts and student answers, markA/markB, default isAprove as "No".
- Insert into theoryCourseQueue and theoryQueue for admin processing.
- Insert into theoryTaken(studentID, courseID, examNo).
- Confirm and redirect to Dashboard.

## Database Schema (from script)
- userInfo: id, name, department, email, semester, gender, password, fatherName, hall, image, no_of_exam, total_mark.
- mcqQS: courseID, qsId/qsNo, qs, op1..op4, ans, tag, eTime.
- theoryQS: courseID, qsId/qsNo, qsA, qsB, markA, markB, eTime.
- mcqTaken: studentID, courseID, examNo, mark.
- theoryAns: studentID, courseID, qsNo, qsA, ansA, markA, isAprove, qsB, markB, ansB.
- theoryQueue: courseID, courseName, [count/time fields may exist].
- theoryCourseQueue: student_ID, courseID.
- Additional admin/evaluation supportive tables as per script.

## Class/Function Outlines
- Code-behind partial classes per page: e.g., public partial class MCQExam : Page with handlers Page_Load, submitB_Click, Timer1_Tick.
- Utility functions embedded in pages (e.g., getCourseName in TheoryExam.aspx.cs).

## Error Handling and Validation
- Display alerts via Response.Write("<script>alert(...)</script>").
- Improve: Replace with server-side validation summaries; consistent try/catch around DB operations.

## Performance Considerations
- Batch queries where possible; avoid opening/closing connections between each question load.
- Cache course lists per semester; reduce repeated DB hits in StartExam.
- Use parameterized queries and indexes on frequently filtered columns.

## Security Considerations
- Replace string concatenation in SQL with SqlCommand parameters throughout.
- Hash and salt passwords; currently stored in plain text.
- Validate session variables before use; fix null checks (e.g., Session["_ID"]).

## Maintainability
- Extract DB access into helper class or repository pattern for reuse and testing.
- Centralize constants like connection string names and course mappings.

## References
- MCQExam.aspx.cs, TheoryExam.aspx.cs, StartExam.aspx.cs, LoginPage.aspx.cs, SignUpPage.aspx.cs, Admin*.aspx.cs files, Web.config, SQL schema script.
