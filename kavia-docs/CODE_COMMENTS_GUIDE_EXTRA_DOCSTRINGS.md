# XML Documentation Examples and Templates

## Class-Level Example (MCQExam.aspx.cs)
```csharp
/// <summary>
/// Provides interaction logic for the MCQ exam page. Handles question loading, timing, answer gathering, and submission.
/// </summary>
/// <remarks>
/// Requires Session["_Course"] to be set by StartExam.aspx. Uses Session to store question text and correct answers.
/// </remarks>
public partial class MCQExam : System.Web.UI.Page
{
}
```

## Method-Level Examples

Page_Load:
```csharp
/// <summary>
/// Loads MCQ questions on initial request and configures the exam timer.
/// </summary>
/// <param name="sender">Page object.</param>
/// <param name="e">Event arguments.</param>
/// <exception cref="InvalidOperationException">Thrown when course is not selected.</exception>
protected void Page_Load(object sender, EventArgs e)
{
    // ...
}
```

Submit handler:
```csharp
/// <summary>
/// Validates selected answers, calculates the score, writes the result to the database, and transitions to the result page.
/// </summary>
/// <param name="sender">Submit button control.</param>
/// <param name="e">Event arguments.</param>
/// <remarks>
/// Uses ADO.NET to insert into mcqTaken. Replace string concatenation with parameterized queries in production.
/// </remarks>
protected void submitB_Click(object sender, EventArgs e)
{
    // ...
}
```

Theory evaluation helper:
```csharp
/// <summary>
/// Enqueues a theory answer set for evaluation and records exam participation.
/// </summary>
/// <param name="studentId">Student unique ID.</param>
/// <param name="courseId">Course ID (e.g., CSE-1101).</param>
/// <param name="examNo">Exam number for the course.</param>
/// <exception cref="SqlException">Database errors encountered during insert operations.</exception>
private void QueueTheoryForEvaluation(string studentId, string courseId, int examNo)
{
    // ...
}
```

## Parameter and Return Documentation
Use <param> tags for each parameter and <returns> for non-void methods. Document possible <exception> types that can be thrown.

## Exception Documentation
Document known exceptions you explicitly throw or expect to bubble up. Provide guidance on when they occur.

## See Also
- CODE_COMMENTS_GUIDE.md for inline comment guidance.
- ARCHITECTURE.md for component and flow understanding.

