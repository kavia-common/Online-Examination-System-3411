# C# XML Documentation Comments Guide

## Purpose
Use C# XML documentation comments to describe classes, methods, parameters, return values, and exceptions. This enables IntelliSense, improves maintainability, and helps generate API documentation.

## Conventions
- Place XML comments immediately above the symbol (class, method, property).
- Use <summary>, <param>, <returns>, <exception>, <remarks>, and <example>.
- Keep summaries concise and imperative.
- Document exceptions that callers should handle.
- Update comments when behavior changes.

## Recommended Tags
- <summary> One- or two-sentence overview.
- <param name="..."> Describe purpose, constraints, and expected format.
- <returns> Clarify return type semantics; note nullability.
- <exception cref="..."> When thrown; include conditions.
- <remarks> Longer notes, side effects, session usage, and DB interactions.
- <example> Basic usage snippet.

## Examples

### LoginPage.aspx.cs
```csharp
/// <summary>
/// Handles authentication for students and teachers, validating credentials
/// against the database and establishing session state.
/// </summary>
public partial class LoginPage : System.Web.UI.Page
{
    /// <summary>
    /// Attempts to authenticate the user using provided credentials,
    /// establishing session values on success and redirecting to the dashboard.
    /// </summary>
    /// <param name="username">The username entered in the login form.</param>
    /// <param name="password">The plaintext password to validate.</param>
    /// <exception cref="UnauthorizedAccessException">
    /// Thrown when credentials are invalid after verification.
    /// </exception>
    protected void btnLogin_Click(object sender, EventArgs e)
    {
        // ...
    }
}
```

### StartExam.aspx.cs
```csharp
/// <summary>
/// Initializes exam selection based on the student's semester and enrollment,
/// preventing duplicate attempts for already taken exams.
/// </summary>
public partial class StartExam : System.Web.UI.Page
{
    /// <summary>
    /// Binds available courses to the dropdown for the current user.
    /// </summary>
    /// <remarks>
    /// Requires Session["userId"] and Session["semester"] to be populated.
    /// Queries the database using the configured connection string.
    /// </remarks>
    protected void BindCoursesForUser()
    {
        // ...
    }
}
```

### MCQExam.aspx.cs
```csharp
/// <summary>
/// Manages the lifecycle of an MCQ exam attempt, including question loading,
/// timing, and answer submission.
/// </summary>
public partial class MCQExam : System.Web.UI.Page
{
    /// <summary>
    /// Loads the current question based on the attempt state and updates the UI.
    /// </summary>
    /// <param name="index">Zero-based question index for the current attempt.</param>
    /// <returns>True if a question was loaded; false when no more questions.</returns>
    protected bool LoadQuestion(int index) { /* ... */ }

    /// <summary>
    /// Submits the user's selected answer and moves to the next question or finalizes the exam.
    /// </summary>
    /// <exception cref="InvalidOperationException">Thrown if no current exam context exists.</exception>
    protected void SubmitAnswer() { /* ... */ }
}
```

### TheoryExam.aspx.cs
```csharp
/// <summary>
/// Handles theory exam display and answer capture, managing timing and submission.
/// </summary>
public partial class TheoryExam : System.Web.UI.Page
{
    /// <summary>
    /// Persists the current answer text for the active question and user.
    /// </summary>
    /// <param name="answer">Free-form answer text provided by the user.</param>
    /// <remarks>Sanitize/encode input to prevent injection attacks.</remarks>
    protected void SaveCurrentAnswer(string answer) { /* ... */ }
}
```

### Admin/ManageQuestions (EditMCQ.aspx.cs, EditTheory.aspx.cs)
```csharp
/// <summary>
/// Supports CRUD operations on exam questions for administrative users.
/// </summary>
/// <remarks>
/// Requires Session["isAdmin"] to be true. Methods interact with the DB for inserts/updates.
/// </remarks>
public partial class EditMCQ : System.Web.UI.Page { /* ... */ }
```

### Repositories/Services (Template)
```csharp
/// <summary>
/// Data access service for exams and questions.
/// </summary>
public interface IExamRepository
{
    /// <summary>
    /// Retrieves questions for the specified exam in the expected order.
    /// </summary>
    /// <param name="examId">The exam identifier.</param>
    /// <returns>Enumerable of questions; empty if none.</returns>
    IEnumerable<Question> GetQuestions(int examId);

    /// <summary>
    /// Records or updates a user's answer for a given question.
/// </summary>
/// <param name="userId">User identifier.</param>
/// <param name="questionId">Question identifier.</param>
/// <param name="answer">Selected option or free text.</param>
void SaveAnswer(int userId, int questionId, string answer);
}
```

## Documentation Checklist
- Every public page class and key helper method has <summary>.
- Event handlers include purpose and preconditions (session values).
- Data access methods document schema expectations and null handling.
- Exceptions are explicitly documented where thrown.
