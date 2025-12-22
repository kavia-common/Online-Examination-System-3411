# Inline Code Comments Guide

## Purpose
Inline comments clarify intent, assumptions, and non-obvious logic across Web Forms code-behind (.aspx.cs), data access routines, and business logic. They should explain “why” over “what,” given that code typically shows “what.”

## General Principles
- Prefer concise, actionable comments near complex logic or side effects (e.g., session state mutations, postback handling, SQL behavior).
- Use comments to mark TODO, HACK, and NOTE with context and next steps.
- Avoid restating obvious code. Focus on business rules, constraints, performance considerations, and security implications.

## Where to Comment in Web Forms
- Code-behind event handlers (Page_Load, Button_Click): clarify ViewState usage, session dependencies, and navigation rationale.
- Data access code: document SQL expectations, parameters, and transaction boundaries (especially with ADO.NET).
- Timer and exam lifecycle logic: clarify time calculations, edge cases, and session expirations.
- Admin workflows: explain preconditions for editing questions, queues, and evaluation steps.

## Examples

### Example: Page_Load with PostBack
```csharp
protected void Page_Load(object sender, EventArgs e)
{
    // Ensure user is authenticated; redirect otherwise
    if (Session["userId"] == null)
    {
        Response.Redirect("LoginPage.aspx");
        return;
    }

    if (!IsPostBack)
    {
        // First load: populate course list based on student's semester
        // NOTE: This relies on Session["semester"] being set at login.
        BindCoursesForSemester();
    }
    // On postback, rely on ViewState to preserve control state
}
```

### Example: SQL Command with Parameterization
```csharp
// Fetch next MCQ question for the exam attempt
// Assumption: @ExamId and @Index are validated earlier in the flow
using (var con = new SqlConnection(ConfigurationManager.ConnectionStrings["OnlineExamConnectionString"].ConnectionString))
using (var cmd = new SqlCommand(@"SELECT TOP 1 * FROM Questions 
                                  WHERE ExamId = @ExamId 
                                  ORDER BY QuestionIndex OFFSET @Index ROWS", con))
{
    cmd.Parameters.AddWithValue("@ExamId", examId);
    cmd.Parameters.AddWithValue("@Index", index);
    con.Open();
    using (var rdr = cmd.ExecuteReader())
    {
        // Handle no-rows scenario: end of question set
    }
}
```

### Example: Timer Handling
```csharp
// Remaining time is tracked in Session to survive postbacks.
// TODO: Consider persisting to DB for resiliency across server restarts.
TimeSpan remaining = (TimeSpan)Session["remainingTime"];
if (remaining <= TimeSpan.Zero)
{
    // Auto-submit when time expires
    SubmitAndFinalize();
}
```

### Example: Admin Edit Flow
```csharp
protected void btnEditMCQ_Click(object sender, EventArgs e)
{
    // Ensure an exam is selected; this page expects Session["examId"] to be set by SetExam.aspx
    if (Session["examId"] == null)
    {
        // TODO: Provide a user-friendly message and redirect to selection page
        Response.Redirect("SetExam.aspx");
        return;
    }
    Server.Transfer("EditMCQ.aspx");
}
```

## Comment Tags
- TODO: actionable item pending
- NOTE: important context or behavior
- HACK: workaround that should be refactored
- PERF: performance-sensitive code path
- SECURITY: security-sensitive logic or validation

## Style
- Keep lines to a reasonable length.
- Use consistent punctuation and capitalization.
- Prefer full sentences for rationale.
