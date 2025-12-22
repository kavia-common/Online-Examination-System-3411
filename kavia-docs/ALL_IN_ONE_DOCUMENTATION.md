# 📚 Consolidated Project Documentation

Below is a single, ready-to-deliver document that merges all generated files (README, Architecture, Workflows, Contributing, and Code Commenting/Docstrings guides) into one cohesive reference.

---

# Online Examination System – Complete Documentation

Version: 1.0

Repository: Online-Examination-System-3411

Technology: ASP.NET Web Forms (.NET Framework), Bootstrap, IIS/ASP.NET Dev Server


1. Tool Overview and Purpose

The Online Examination System enables educational institutions to create and manage online exams for multiple courses. Teachers (Admins) can create MCQ and theory questions, define exams, evaluate theory responses, and publish results. Students can register, enroll in courses, take timed exams, view scores, ranks, and download result summaries.

Key audiences:
- Admin (Teacher): Create/edit exams, manage questions, evaluate theory answers, view leaderboards.
- Student: Register, enroll, take exams, review results and rankings.

Business value:
- Digitizes exam management end-to-end and reduces manual effort.
- Ensures consistent evaluation and timely results publication.
- Provides transparency via leaderboards and downloadable summaries.


2. Features

- Role-based authentication (Student, Admin)
- Admin panel: create/edit MCQ and theory questions, set exams per course
- Timed exams: MCQ and theory sections
- Student registration and course enrollment
- Leaderboards and result pages with scores and rankings
- Theory answer evaluation workflow: pending queues, grading UI for teachers
- Download PDF result summary via dedicated page


3. Installation

Prerequisites:
- Windows with .NET Framework SDK (target compatible with project)
- Visual Studio (recommended) or msbuild
- IIS or IIS Express/ASP.NET Development Server
- SQL Server/LocalDB if project uses a database (configure connection strings accordingly)

Steps:
1) Clone the repository.
2) Open the solution in Visual Studio.
3) Restore NuGet packages (Visual Studio will prompt automatically).
4) Configure database connection strings in Web.config.
5) Build the solution.
6) Run via IIS Express or configure site in IIS.


4. Setup and Configuration

Environment variables: none currently defined in .env. If you introduce external services later (e.g., PDF libraries with keys), document them here and update Web.config accordingly.

Configuration files:
- Web.config: database connection strings, app settings (e.g., exam duration defaults, file upload limits).
- Machine.config/IIS site settings as applicable.

Database setup:
- Ensure the database schema is created/migrated. If scripts are present, run them or use EF migrations if applicable.


5. How to Run

- From Visual Studio: Press F5 to run with IIS Express.
- From IIS: Create an application pointing to Online-Examination-System-3411/OnlineExamSystem and bind a site.
- The preview system may auto-start on port 3001 for this workspace.

Default URLs:
- /Login.aspx – user login
- /Admin/* – admin features
- /Student/* – student dashboard and exam pages


6. Basic Usage

As Admin:
- Log in as Admin.
- Create Courses.
- Add Questions (MCQ/Theory) to the question bank.
- Compose Exams (select course, question sets, durations, schedules).
- After exams, review Pending Theory Answers -> grade -> publish results.

As Student:
- Register and log in.
- Enroll in desired courses.
- Start the scheduled exam (timer enforced).
- Submit answers; view results and leaderboard once published.


7. Supported Platforms and Versions

- ASP.NET Web Forms on .NET Framework (classic)
- Runs on Windows + IIS/IIS Express
- Supported browsers: modern Chromium-based, Firefox, Edge; IE not recommended.


8. License

Provide your chosen license (MIT/Apache-2.0/Proprietary). Update LICENSE file and reflect here.


9. Project Structure

Online-Examination-System-3411/
├─ OnlineExamSystem/                (ASP.NET Web Forms site root)
│  ├─ MasterPages/                 (Site master pages)
│  ├─ Pages/                       (Content pages: Login, Dashboard, Exams, Admin)
│  ├─ Controls/                    (User controls)
│  ├─ App_Code/                    (Business/data helper classes if used)
│  ├─ Scripts/                     (JS files)
│  ├─ Styles/                      (CSS/Bootstrap)
│  ├─ Web.config                   (App configuration)
│  └─ Global.asax                  (Application events)
├─ kavia-docs/                     (Documentation set)
│  ├─ README.md
│  ├─ ARCHITECTURE.md
│  ├─ WORKFLOWS.md
│  ├─ CONTRIBUTING.md
│  ├─ CODE_COMMENTS_GUIDE.md
│  └─ CODE_COMMENTS_GUIDE_EXTRA_DOCSTRINGS.md
└─ .env                            (currently empty)


10. Architecture

10.1 System Context
- Client: Browser (students/admins)
- Web Application: ASP.NET Web Forms (UI + server logic)
- Database: SQL Server/LocalDB storing users, courses, questions, exams, attempts, results

10.2 Logical Components
- Authentication & Authorization: login, roles (Student, Admin)
- Course & Enrollment Management
- Question Bank: MCQ and Theory
- Exam Management: assemble exams, schedule, duration, sections
- Exam Delivery: timed pages, navigation, submission
- Evaluation: auto-grade MCQ; manual grading queue for theory
- Results & Leaderboard: score calculation, ranking, publish
- PDF Generation: summary/result export

10.3 High-Level Diagram (Mermaid)

```mermaid
flowchart LR
  Browser[User Browser]\n  UI[ASP.NET Web Forms UI]\n  Auth[Auth & Roles]\n  QBank[Question Bank]\n  Exams[Exam Mgmt]\n  Delivery[Exam Delivery]\n  Eval[Evaluation]\n  Results[Results & Leaderboard]\n  PDF[PDF Export]\n  DB[(SQL Database)]

  Browser --> UI
  UI --> Auth
  UI --> QBank
  UI --> Exams
  UI --> Delivery
  UI --> Results
  UI --> PDF

  Auth --> DB
  QBank --> DB
  Exams --> DB
  Delivery --> DB
  Eval --> DB
  Results --> DB
  PDF --> DB
```

10.4 Data Flow (Exam Attempt)
- Student starts timed exam
- System loads questions for course/exam
- Student submits answers progressively or at end
- MCQ auto-graded; theory answers queued for evaluation
- Final result calculated post-grading; leaderboard updated

10.5 Sequence (Theory Evaluation)
1) Teacher opens Pending Theory Queue
2) System fetches ungraded submissions
3) Teacher reviews, enters marks, submits
4) System updates result
5) Leaderboard recalculates ranks
6) Student sees updated score and can download PDF

10.6 Design Decisions
- Web Forms Master/Content for consistency and reuse
- Role-based navigation to simplify UX per user type
- Server-side controls and ViewState for classic Web Forms state management
- Auto-grading for MCQ; manual grading pipeline for theory
- PDF export to provide shareable artifacts


11. Configuration & Environment

Required software:
- Windows, .NET Framework, Visual Studio, IIS/IIS Express

Dependencies:
- Bootstrap (styles)
- PDF library (choose one such as iTextSharp or SelectPDF; document once integrated)

Environment variables:
- None currently in .env. If introducing services (email, storage, PDF API), document keys here and in Web.config appSettings.

Database configuration:
- ConnectionStrings in Web.config (e.g., DefaultConnection)
- Recommended: use parameterized queries or ORM (ADO.NET, EF) to prevent injection


12. API or Interface Documentation

UI Pages (examples):
- Login.aspx: authenticate user; redirects based on role
- Admin/Dashboard.aspx: entry to Courses, Questions, Exams, Evaluation
- Admin/Questions.aspx: CRUD for MCQ/Theory
- Admin/Exams.aspx: create/edit exams (duration, course, question sets)
- Admin/Evaluate.aspx: list pending theory answers, grading interface
- Student/Register.aspx: registration
- Student/Courses.aspx: enroll in courses
- Student/Exams.aspx: list available exams
- Student/Exam.aspx: take timed exam
- Results/Leaderboard.aspx: rankings across completed exams
- Results/DownloadPdf.aspx: download result summaries

Input/Output & Errors:
- Validation messages rendered on page via server controls
- Form inputs validated on client (basic) and server (authoritative)
- Error handling via global error page and per-page validation summaries


13. Contribution & Extension Guidelines

Development workflow:
- Fork and branch: feature/<name> or fix/<name>
- Commit style: Conventional Commits (feat:, fix:, docs:, refactor:, test:, chore:)
- Pull Requests: include summary, screenshots for UI, test notes

Coding standards:
- C# style: use meaningful names, early returns for guards, avoid deep nesting
- Web Forms: prefer server controls only when beneficial; keep code-behind focused on orchestration; move reusable logic to App_Code/services
- Security: parameterized queries; validate inputs; role checks on every sensitive action

Adding features:
- Extend data model and update DAL/ORM
- Add pages/controls and route via Master
- Add server-side validation and appropriate authorization
- Update docs (README, ARCHITECTURE, WORKFLOWS)

Testing:
- Unit test core logic in App_Code/services where possible
- Manual test critical flows (login, exam delivery, grading)


14. Inline Code Comments Guide

When to comment:
- Complex logic, non-obvious decisions, security-sensitive code, workarounds
How to comment:
- Explain intent and rationale; avoid duplicating the code
- Use TODO/FIXME tags with context

Examples (C# code-behind):

```csharp
// Validate time window to prevent starting outside schedule
if (!IsWithinExamWindow(exam))
{
    // Inform user without revealing internal scheduling rules
    ShowMessage("Exam is not currently available.");
    return;
}
```

```csharp
// Tie MCQ auto-grading to selected answers; theory is graded separately in Evaluate.aspx
var mcqScore = GradeMcq(answers);
// TheoryScore remains null until teacher evaluation completes
```


15. Function & Class Documentation (Docstrings/XML Comments)

C# XML summary example:

```csharp
/// <summary>
/// Calculates the score for a completed MCQ section.
/// </summary>
/// <param name="answers">Student's selected options by question ID.</param>
/// <returns>Total points for MCQ questions.</returns>
public int GradeMcq(Dictionary<int, int> answers) { ... }
```

For pages (code-behind):

```csharp
/// <summary>
/// Loads pending theory submissions for the grading queue.
/// Ensures only Admin users can access this page.
/// </summary>
protected void Page_Load(object sender, EventArgs e) { ... }
```


16. Business Workflows

Template applied to core flows.

16.1 Workflow: Student Exam Participation
- Actors: Student, System, Admin
- Trigger: Student chooses an available scheduled exam
- Preconditions: Student authenticated and enrolled; exam open and within time window
- Steps:
  1) Student starts the exam
  2) System displays questions and starts timer
  3) Student answers and submits
  4) System auto-grades MCQ; queues theory answers for review
  5) Admin later completes theory grading
  6) System publishes final result and updates leaderboard
- Postconditions: Score and rank available; PDF summary downloadable
- Business Value: Streamlined testing with quick objective scoring and auditable results

16.2 Workflow: Admin Creates and Schedules Exam
- Actors: Admin, System
- Trigger: Admin decides to conduct an exam for a course
- Preconditions: Course exists; question bank prepared
- Steps:
  1) Admin selects course and exam parameters (duration, date)
  2) Admin selects questions (MCQ/Theory) from bank
  3) System saves exam configuration and schedules availability
- Postconditions: Exam listed for enrolled students during window
- Business Value: Efficient authoring and scheduling of assessments

16.3 Workflow: Theory Answer Evaluation
- Actors: Admin, System
- Trigger: New theory submissions pending
- Preconditions: Exam completed by students
- Steps:
  1) Admin opens pending evaluation queue
  2) System shows anonymized or identified submissions
  3) Admin reviews answers and assigns scores
  4) System updates results and recalculates rankings
- Postconditions: Final results available to students
- Business Value: Controlled manual grading with traceability

16.4 Workflow: Result Reporting and Leaderboard
- Actors: Student, Admin, System
- Trigger: After grading completion
- Preconditions: Grading completed for attempt
- Steps:
  1) System aggregates scores
  2) Leaderboard ranks students by score/time
  3) Student views results and downloads PDF summary
- Postconditions: Results persist for audits and transcripts
- Business Value: Transparency and motivation via rankings and shareable reports


17. Traceability: Modules to Business Processes

- Auth/Login.aspx → User Authentication
- Admin/Questions.aspx → Question Bank Management
- Admin/Exams.aspx → Exam Authoring & Scheduling
- Student/Exam.aspx → Exam Delivery
- Admin/Evaluate.aspx → Theory Evaluation
- Results/Leaderboard.aspx → Ranking & Reporting
- Results/DownloadPdf.aspx → Result Summaries


18. Error Handling & Security

- Authentication/Authorization checks on every sensitive page
- Input validation both client- and server-side
- Parameterized queries to prevent SQL injection
- Graceful error messaging without leaking internals
- Logging of critical events (logins, grading actions)


19. Maintenance & Operations

- Backup database regularly
- Monitor application logs for failed logins and grading anomalies
- Update dependencies (NuGet, Bootstrap) periodically
- Regression test core flows after updates


20. Future Enhancements

- Two-factor authentication for Admins
- Rich analytics for cohort performance
- Automated proctoring and integrity checks
- Bulk import/export for questions and results
- Pluggable PDF engine with templating

---

End of consolidated documentation.
