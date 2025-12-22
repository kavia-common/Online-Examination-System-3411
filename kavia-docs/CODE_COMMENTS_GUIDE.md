# Code Comments and Documentation Guide (ASP.NET Web Forms)

## Overview
This guide explains how to add high-quality inline code comments and XML documentation in a C# ASP.NET Web Forms application. It focuses on code-behind logic, data access operations, and business workflows typical to this Online Examination System.

## Inline Code Comments (What and Where)
Inline comments are crucial to communicate intent and decisions. Add them:
- Around complex logic that manipulates state via Session, ViewState, or server controls.
- Where SQL commands are constructed or parameters are bound, explaining the query’s purpose and expected results.
- Near navigation actions (Server.Transfer/Response.Redirect), clarifying why control is transferred to a particular page.
- For timer or time-based logic, describing how time windows are computed.
- When handling exceptions, clarifying what failures are expected and what the fallback behavior is.
- Around any security checks (e.g., role checks, session validations), noting the expected user roles and implications.

Prefer “why” over “what”: brief comments that justify decisions, constraints, or assumptions. Keep comments up-to-date with code changes.

### Examples
C# code-behind (MCQ evaluation):
```csharp
// Compute total correct answers for the current MCQ exam.
// Each RadioButtonList corresponds to one question; compare with the correct answer stored in Session.
int mark = 0;
if (RadioButtonList1.SelectedIndex > -1 && RadioButtonList1.SelectedItem.Text == a1) { mark++; }
// ...repeat for other questions
```

C# data access:
```csharp
// Insert MCQ result for the current student and course.
// TODO: Replace inline SQL with parameterized queries to prevent SQL injection.
using (var con = new SqlConnection(CS))
using (var cmd = new SqlCommand("insert into mcqTaken (studentID, courseID, examNo, mark) values (@sid, @cid, @examNo, @mark)", con))
{
    cmd.Parameters.AddWithValue("@sid", sNo);
    cmd.Parameters.AddWithValue("@cid", crsNo);
    cmd.Parameters.AddWithValue("@examNo", 1);
    cmd.Parameters.AddWithValue("@mark", mark);
    con.Open();
    cmd.ExecuteNonQuery();
}
```

UI state and navigation:
```csharp
// Transfer to the dashboard after successful login to initialize student workflow
Server.Transfer("Dashboard.aspx", true);
```

## XML Documentation Comments (Docstrings)
Use C# XML documentation comments for:
- Classes and partial classes (e.g., code-behind pages)
- Public methods and event handlers
- Methods performing data access or business logic
- Parameters, return values, and thrown exceptions

Enable “XML documentation file” in project settings if you want generated XML for tooling.

### Templates

Class template:
```csharp
/// <summary>
/// Code-behind for the MCQExam page. Handles loading questions, tracking timer, and evaluating responses.
/// </summary>
/// <remarks>
/// This page expects Session["_Course"] and uses Session to store loaded questions and correct answers.
/// </remarks>
public partial class MCQExam : System.Web.UI.Page
{
}
```

Method template with parameters and exceptions:
```csharp
/// <summary>
/// Handles submission of MCQ answers, computes score, persists result, and navigates to the result page.
/// </summary>
/// <param name="sender">The source control invoking the event.</param>
/// <param name="e">Event arguments.</param>
/// <exception cref="InvalidOperationException">Thrown when required session state is missing.</exception>
protected void submitB_Click(object sender, EventArgs e)
{
    // implementation...
}
```

Utility method:
```csharp
/// <summary>
/// Returns a human-readable course name given a course code.
/// </summary>
/// <param name="courseID">Course code, e.g., "CSE-1101".</param>
/// <returns>Course name for display in the UI.</returns>
protected string GetCourseName(string courseID)
{
    // ...
}
```

Event handlers:
```csharp
/// <summary>
/// Timer tick event updates remaining time label and detects timeout.
/// </summary>
/// <param name="sender">Timer control.</param>
/// <param name="e">Event args.</param>
protected void Timer1_Tick(object sender, EventArgs e)
{
    // ...
}
```

## Where to Place Documentation
- Above class declarations in .aspx.cs files.
- Above each handler: Page_Load, Button_Click, Timer_Tick, SelectedIndexChanged, etc.
- Above private helper methods to clarify purpose and expected side effects (e.g., populating controls, loading data).
- For ADO.NET code blocks, add inline comments or summarize in method-level XML comments.

## Page-Specific Examples

Exam creation (TheorySet.aspx.cs):
```csharp
/// <summary>
/// Adds new theory questions for the selected course and exam number.
/// Performs basic validation on input fields before persisting to the database.
/// </summary>
protected void addTheoryQsButton_Click(object sender, EventArgs e)
{
    // Validate inputs
    // Save to theoryQS table
    // Provide user feedback
}
```

MCQ evaluation (MCQExam.aspx.cs):
```csharp
/// <summary>
/// Loads MCQ questions for the selected course and initializes Session-based timer on first load.
/// </summary>
protected void Page_Load(object sender, EventArgs e)
{
    // Load questions for qs 1..5; store correct answers in Session
    // Initialize timer on first load
}
```

## Comment Quality Checklist
- Is the comment necessary to understand intent or rationale?
- Is it concise and accurate?
- Does it avoid duplicating what the code already clearly shows?
- Is it updated along with code changes?
- Does it highlight security, performance, or correctness considerations?

