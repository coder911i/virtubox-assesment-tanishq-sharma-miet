# Potential Bugs / Risk Areas

> **Important:** These are potential defects identified from requirement analysis only. The application was not executed, so these are risk hypotheses rather than confirmed bugs.

| ID | Potential bug / risk | Severity | Reason / impact |
|---|---|---|---|
| BUG-01 | Duplicate email registration may be allowed. | Major | Can create duplicate accounts and lead to inconsistent user data or login confusion. |
| BUG-02 | Invalid credentials could cause an unhandled server/UI error instead of a controlled login failure. | Critical | Login is a core function; crashes can make the application unavailable and may expose implementation details. |
| BUG-03 | A user may access protected task functionality without being authenticated. | Critical | Could expose or modify task data without authorization. |
| BUG-04 | User A may be able to view, edit or delete User B's tasks. | Critical | Serious authorization and privacy issue with potential cross-user data manipulation. |
| BUG-05 | A deleted task may reappear after refreshing the task list. | Major | Indicates persistence or UI/database synchronization failure and can mislead users about the state of their data. |
| BUG-06 | An edited task may look updated in the UI but revert after refresh. | Major | Changes may not be persisted correctly, causing data loss and inconsistent state. |
| BUG-07 | Blank/invalid task data may be accepted. | Major | Creates incomplete or invalid records and reduces the quality/reliability of task data. |
| BUG-08 | Very long or unexpected input may break validation, layout or backend processing. | Major | Can cause poor UX, application errors, or potentially unsafe input handling. |
| BUG-09 | Database/server failure may return a success message even though the operation failed. | Major | Users may believe a task was saved/updated/deleted when the database state says otherwise. |
| BUG-10 | Delete may happen without confirmation or repeated delete requests may leave an inconsistent UI state. | Minor | Can cause accidental deletion and confusing task-list behaviour. |

## Severity Rationale

- **Critical:** Security, authorization, data privacy, or a core failure that can seriously compromise the application.
- **Major:** Significant functional/data-integrity problem that affects normal usage but does not necessarily compromise the whole system.
- **Minor:** Limited usability or lower-impact functional issue.

## Highest-Risk Areas to Test First

1. Authentication and authorization
2. Cross-user task/data isolation
3. Database persistence after create/edit/delete
4. Failure handling for database/server errors
5. Required-field and input validation
6. Destructive delete behaviour
