# RULES.md — Task Management System

## 1. General Development Rules

- The application must be developed using Laravel and Blade.
- Follow Laravel naming conventions and project structure.
- Use Git and GitHub for version control.
- Keep code readable, reusable, and organized.
- Do not commit passwords, API keys, or other secret credentials.
- Update project documentation when important features change.

## 2. User Account Rules

- Each user must have a unique email address.
- Users must authenticate before accessing protected pages.
- Users can view and update only their own profile.
- Users must not access another user's private data without authorization.

## 3. Project Rules

- A user can create and manage multiple projects.
- The user who creates a project becomes its owner.
- Only the project owner can manage project invitations.
- A project owner can invite registered users using their email addresses.
- A user must accept an invitation before becoming a project member.
- Pending or rejected invitations must not grant project membership.
- Only authorized users can view or manage project information.
- Project deletion and other sensitive actions must be restricted to authorized users.

## 4. Invitation Rules

- Invitations must be associated with a project and an invited user.
- Each invitation must have a status: Pending, Accepted, or Rejected.
- An invitation must be accepted or rejected by its intended recipient.
- Unauthorized users cannot respond to another user's invitation.
- Duplicate active invitations to the same user for the same project should be prevented.
- Only accepted members can access the project as team members.

## 5. Task Rules

- A user can create personal tasks.
- Project tasks must belong to an existing project.
- Project tasks can be assigned only to eligible project members.
- Each task must have a title.
- Task descriptions and due dates may be optional.
- Task priority must be Low, Medium, or High.
- Task status must be To Do, In Progress, or Completed.
- Users can update or delete tasks only when authorized.
- Task changes must not allow users to access unauthorized projects.

## 6. Authorization Rules

- Authentication and authorization must be checked on the server.
- Hiding a button is not sufficient to protect an action.
- Controllers must verify permissions before displaying, updating, or deleting protected records.
- Users must not access project information by changing a URL or record ID.
- Validation must be applied to incoming form data.

## 7. Database Rules

- Use migrations to define database tables.
- Use foreign keys where appropriate.
- Use appropriate indexes and unique constraints.
- Maintain valid relationships between users, projects, invitations, and tasks.
- Use Laravel Eloquent relationships where appropriate.
- Prevent orphaned records and maintain data integrity.

## 8. GitHub Rules

- Keep the repository public for the project submission.
- Use meaningful commit messages.
- Commit related changes in logical groups.
- Keep README.md updated with project information and setup instructions.
- Never commit `.env` files or sensitive credentials.
- Review changes before pushing them to the repository.

## 9. Documentation Rules

- Keep PRD.md updated when project requirements change.
- Keep DESIGN.md updated when the interface structure changes.
- Keep DATABASE.md updated when the database schema changes.
- Keep FLOW.md updated when the application workflow changes.
- Use Markdown headings and lists for clear documentation.

## 10. Error Handling

- Display understandable validation and error messages.
- Handle missing records appropriately.
- Prevent unauthorized operations.
- Avoid exposing passwords, secrets, or sensitive technical details in error messages.
