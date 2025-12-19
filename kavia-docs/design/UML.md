# UML Diagrams and Explanations

## Use Case Diagram (Textual)
```mermaid
graph TD
  Student["Actor: Student"] --> UC1["Use Case: Register & Login"]
  Student --> UC2["Use Case: Start Exam"]
  Student --> UC3["Use Case: Take MCQ Exam"]
  Student --> UC4["Use Case: Take Theory Exam"]
  Student --> UC5["Use Case: View Results & Leaderboard"]

  Admin["Actor: Admin/Teacher"] --> UC6["Use Case: Create/Edit Questions"]
  Admin --> UC7["Use Case: Manage Exams"]
  Admin --> UC8["Use Case: Evaluate Theory Answers"]
  Admin --> UC9["Use Case: Publish/Export Results"]
```

## Class Diagram (Simplified logical view)
```mermaid
classDiagram
  class LoginPage {
    +Page_Load()
    +loginButton_Click()
  }
  class SignUpPage {
    +Page_Load()
    +signUpB_Click()
  }
  class StartExam {
    +Page_Load()
    +GridView1_SelectedIndexChanged()
    +GridView2_SelectedIndexChanged()
  }
  class MCQExam {
    +Page_Load()
    +submitB_Click()
    +Timer1_Tick()
  }
  class TheoryExam {
    +Page_Load()
    +submitB_Click()
    +Timer1_Tick()
  }
  class AdminPanel
  class MCQSet
  class TheorySet
  class EditMCQ
  class EditTheory
  class AdminQueue
  class AdminCourseQueue
  class Leaderboard
  class ExamResult

  LoginPage --> StartExam : sets Session and navigates
  SignUpPage --> LoginPage : post-registration redirect
  StartExam --> MCQExam : MCQ flow
  StartExam --> TheoryExam : Theory flow
  MCQExam --> ExamResult : after submit
  TheoryExam --> AdminQueue : enqueues
  AdminQueue --> ExamResult : after evaluation
```

## Sequence Diagram: MCQ Exam Flow
```mermaid
sequenceDiagram
  participant S as Student
  participant SE as StartExam.aspx
  participant M as MCQExam.aspx
  participant DB as SQL Server

  S->>SE: Select course and MCQ type
  SE->>DB: Verify mcqQS availability
  SE-->>S: Navigate to MCQExam
  S->>M: Load page
  M->>DB: Query mcqQS for qs 1..5
  M-->>S: Render questions and timer
  S->>M: Submit answers
  M->>DB: Insert into mcqTaken
  M-->>S: Redirect to ExamResult
```

## Sequence Diagram: Theory Exam Submission
```mermaid
sequenceDiagram
  participant S as Student
  participant T as TheoryExam.aspx
  participant DB as SQL Server
  participant A as AdminQueue

  S->>T: Load page
  T->>DB: Load theoryQS pairs
  T-->>S: Render questions and timer
  S->>T: Submit answers
  T->>DB: Insert theoryAns x5
  T->>DB: Insert theoryCourseQueue, theoryQueue, theoryTaken
  T-->>S: Confirmation & redirect
  A->>DB: Later evaluates and updates approvals/marks
```

## Activity Diagram: Login and Exam Start
```mermaid
flowchart TD
  A["Open LoginPage"] --> B{"Valid credentials?"}
  B -- Yes --> C["Set Session and go to Dashboard"]
  B -- No --> A
  C --> D["Open StartExam"]
  D --> E{"Questions available?"}
  E -- MCQ Yes --> F["Go to MCQExam"]
  E -- Theory Yes --> G["Go to TheoryExam"]
  E -- None --> H["Notify and stay on StartExam"]
```

## Component Diagram
```mermaid
graph LR
  UI["ASPX Pages + Bootstrap"] --> BL["Code-behind (C#)"]
  BL --> DAL["ADO.NET"]
  DAL --> DB["SQL Server"]
```

## Deployment Diagram
```mermaid
graph TD
  Client["Web Browser"] --> IIS["IIS on Windows Server"]
  IIS --> App["ASP.NET Web Forms App (.NET Framework 4.8)"]
  App --> SQL["SQL Server Instance"]
```

## Explanations
- The use case diagram highlights distinct user goals for students and admins.
- The class diagram shows page-level classes with their key handlers and navigation relationships.
- Sequence diagrams detail the runtime interactions during MCQ and theory exam flows.
- The activity diagram shows decisions during login and exam initiation.
- Component and deployment diagrams illustrate the layered architecture and runtime topology.

## References
- Code-behind pages: LoginPage.aspx.cs, SignUpPage.aspx.cs, StartExam.aspx.cs, MCQExam.aspx.cs, TheoryExam.aspx.cs, Admin*.aspx.cs
- Web.config and project file for platform and dependencies
- SQL schema script for data structures
