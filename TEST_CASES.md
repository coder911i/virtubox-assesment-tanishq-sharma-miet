# Test Case Design

## Application Under Test
Task Management Application

The application supports user registration/login and, for logged-in users, creating, viewing, editing and deleting tasks. Tasks are stored in a database and displayed in a list.

## Test Cases

| ID | Module | Test case / steps | Expected result | Type |
|---|---|---|---|---|
| REG-01 | Registration | Enter valid name, email and password and submit. | Account is created and user receives the expected success/redirect behaviour. | Positive |
| REG-02 | Registration | Leave each mandatory field blank one at a time. | Relevant validation message is displayed and registration is blocked. | Negative |
| REG-03 | Registration | Enter an invalid email such as `abc@`. | Email validation is shown and registration is blocked. | Negative |
| REG-04 | Registration | Register with an email that already exists. | Duplicate registration is rejected with a clear error. | Negative |
| REG-05 | Registration | Enter values at the minimum and maximum allowed field lengths. | Boundary values are handled according to the defined validation rules. | Edge |
| REG-06 | Registration | Add leading/trailing spaces to name/email fields. | Input is handled consistently and unintended spaces do not create incorrect/duplicate data. | Edge |
| REG-07 | Registration | Enter special characters/unexpected input in text fields. | Input is validated safely and the application does not break. | Negative |
| LOG-01 | Login | Login with valid registered credentials. | User is authenticated and reaches the protected task area. | Positive |
| LOG-02 | Login | Use correct email with an incorrect password. | Login is rejected with a clear, non-sensitive error message. | Negative |
| LOG-03 | Login | Use an unregistered email. | Login is rejected safely without exposing unnecessary account information. | Negative |
| LOG-04 | Login | Leave email/password blank and submit. | Required-field validation appears and login is not submitted. | Negative |
| LOG-05 | Login | Try email with different casing. | Behaviour follows the application's defined credential/email case rules consistently. | Edge |
| LOG-06 | Login | Enter very long/unusual credential input. | Input is safely handled; UI/API does not crash or become unusable. | Edge |
| TSK-01 | Create | Create a task with valid required information. | Task is saved and appears in the task list. | Positive |
| TSK-02 | Create | Submit a task with required title/details blank. | Validation is displayed and task is not created. | Negative |
| TSK-03 | Create | Create multiple valid tasks. | All valid tasks are saved and displayed correctly. | Positive |
| TSK-04 | Create | Use maximum permitted task-field length. | Boundary value is accepted or rejected according to requirements without error. | Edge |
| TSK-05 | View | Open task list after creating tasks. | Correct saved tasks and their information are displayed. | Positive |
| TSK-06 | View | Open task list when the user has no tasks. | A useful empty-state message is shown and the page remains usable. | Edge |
| TSK-07 | View | Refresh after creating a task. | Task remains present and matches persisted database data. | Positive |
| TSK-08 | View | Verify task ordering/display after several tasks are created. | Tasks are displayed consistently according to the application's defined behaviour. | Edge |
| TSK-09 | Edit | Open an existing task, change valid data and save. | Updated values are displayed and persisted. | Positive |
| TSK-10 | Edit | Clear a required field and save. | Update is rejected and validation is displayed. | Negative |
| TSK-11 | Edit | Enter maximum/boundary values while editing. | Boundary values are handled according to requirements. | Edge |
| TSK-12 | Edit | Edit a task and refresh the page. | Updated values remain after refresh, proving persistence. | Positive |
| TSK-13 | Delete | Delete an existing task and confirm. | Task disappears from the list and is removed from persistence. | Positive |
| TSK-14 | Delete | Start deletion and cancel confirmation. | Task remains unchanged. | Negative/Edge |
| TSK-15 | Delete | Delete the last remaining task. | Empty state is shown correctly after deletion. | Edge |
| TSK-16 | Delete | Attempt repeated deletion of an already deleted/non-existent task. | Request is handled gracefully without crash or inconsistent UI. | Edge |
| VAL-01 | Validation | Submit forms with whitespace-only required values. | Whitespace-only values are rejected where the field is required. | Negative |
| VAL-02 | Validation | Enter HTML/script-like input into task fields. | Input is safely handled and not executed as code. | Negative |
| VAL-03 | Error Handling | Simulate server/database failure during task creation. | User gets a useful error; no false success or partial/corrupt record is created. | Negative |
| VAL-04 | Error Handling | Simulate failure during edit/delete. | User gets an appropriate error and existing data remains consistent. | Negative |
| AUTH-01 | Authentication | Try to open protected task functionality without logging in. | Access is blocked or redirected to login. | Negative |
| AUTH-02 | Data Isolation | Login as User A and verify User B's tasks are not visible/editable/deletable. | Each user can access only authorized tasks. | Security/Negative |

## Suggested Execution Order

1. Registration and login smoke tests
2. Authentication and data-isolation checks
3. Create/view/edit/delete happy paths
4. Validation and negative cases
5. Boundary/edge cases
6. Failure handling and persistence checks

## Expected Evidence During Real Execution

For an actual execution cycle, capture screenshots/logs for failed cases, record environment/browser details, and link failures to defect IDs. Since this assessment is based on requirements and the application was not executed, no case above is claimed as an observed defect.
