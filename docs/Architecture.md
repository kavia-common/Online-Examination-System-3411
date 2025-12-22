# Architecture and Flow

## High-Level Architecture
The application is a monolithic ASP.NET Web Forms site that serves both UI and server-side logic. It follows the standard Web Forms model with .aspx pages paired with code-behind files. Data is persisted to SQL Server. Styling is provided via Bootstrap.

### Components
- UI Pages (.aspx + .aspx.cs): Handle user interactions via server controls and postbacks.
- Business Logic (within code-behind, or future Services): Encapsulate workflows (exam lifecycle, evaluation).
- Data Access (ADO.NET within pages today; optional Repositories later): Execute parameterized SQL queries.
- State Management: Session, ViewState, and occasionally cookies or query strings.
- Configuration: Web.config with connectionStrings.
- Styling: Bootstrap CSS.

### Diagram: Container and Components
```mermaid
flowchart LR
    Browser["Browser (Student/Admin)"] --> IIS["IIS/IIS Express"]
    IIS --> WebForms["ASP.NET Web Forms App"]
    WebForms --> UI[".aspx Pages + Code-behind"]
    UI --> Session["Session / ViewState"]
    WebForms --> Data["ADO.NET / Data Access"]
    Data --> SQL["SQL Server Database"]
    UI --> Bootstrap["Bootstrap CSS"]
```

## Data Flow Scenarios

### User Authentication and Dashboard
```mermaid
sequenceDiagram
    participant U as User
    participant L as LoginPage.aspx
    participant DB as SQL Server

    U->>L: Submit credentials
    L->>DB: Validate username/password
    DB-->>L: Valid/Invalid
    alt valid
        L->>U: Set session and redirect to Dashboard.aspx
    else invalid
        L->>U: Show error message
    end
```

### Exam Lifecycle (MCQ)
```mermaid
sequenceDiagram
    participant S as StartExam.aspx
    participant M as MCQExam.aspx
    participant DB as SQL Server

    S->>M: Begin MCQ (course, examId)
    M->>DB: Load first question
    loop For each question
        U->>M: Select answer, Next
        M->>DB: Save answer
    end
    M->>DB: Finalize and compute score
    M->>U: Redirect to ExamResult.aspx
```

### Admin Flow (Question Management)
```mermaid
sequenceDiagram
    participant A as AdminPanel.aspx
    participant E as EditMCQ.aspx/EditTheory.aspx
    participant DB as SQL Server

    A->>E: Navigate to edit questions
    E->>DB: Load questions for exam
    A->>E: Create/Update/Delete question
    E->>DB: Persist changes
```

## Design Considerations

### ViewState and Postbacks
- ViewState stores page and control state between postbacks; avoid large objects to keep payload small.
- Use IsPostBack in Page_Load to separate initialization from postback logic.

### Session Usage
- Session stores user identity, current exam context, and timer metadata.
- Keep session keys consistent and documented; clear or invalidate on logout.

### Timer Handling
- Timers are session-backed with server-side checks on submission.
- Consider persisting remaining time for resiliency if server restarts are a concern.

### Security
- Validate all inputs; use parameterized queries.
- Encode outputs to avoid XSS.
- Restrict admin pages to authorized roles (e.g., check Session["isAdmin"]).

### PDF Generation
- DownloadPdf.aspx contains a code-behind placeholder.
- Implement using Crystal Reports or a .NET PDF library; document data sources and output paths.

## Future Enhancements
- Introduce Services/Repositories to decouple data access from UI.
- Add centralized authentication/authorization helpers.
- Implement Web API endpoints if integrating SPA or external clients.
- Improve timer robustness and client/server synchronization.

## Glossary
- MCQ: Multiple Choice Questions
- Theory Exam: Free-form answers requiring manual evaluation
- Queue: Pending theory answers awaiting grading
