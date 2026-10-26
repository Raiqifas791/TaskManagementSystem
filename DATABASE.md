# DATABASE.md — Task Management System

## 1. Database Overview

The application will use MySQL as its relational database.

The database will store user accounts, projects, project invitations, project memberships, and tasks.

## 2. Database Tables

### 2.1 users

Stores registered user information.

| Column | Type | Description |
|---|---|---|
| id | BIGINT, Primary Key | Unique user ID |
| name | VARCHAR | User's full name |
| email | VARCHAR, Unique | User's email address |
| password | VARCHAR | Hashed password |
| created_at | TIMESTAMP | Record creation time |
| updated_at | TIMESTAMP | Last update time |

Laravel authentication may require additional standard columns, such as email verification and remember token fields.

### 2.2 projects

Stores projects created by users.

| Column | Type | Description |
|---|---|---|
| id | BIGINT, Primary Key | Unique project ID |
| owner_id | BIGINT, Foreign Key | User who owns the project |
| name | VARCHAR | Project name |
| description | TEXT, Nullable | Project description |
| start_date | DATE, Nullable | Project start date |
| due_date | DATE, Nullable | Project deadline |
| created_at | TIMESTAMP | Record creation time |
| updated_at | TIMESTAMP | Last update time |

Relationship:
- Each project belongs to one owner.
- One user can own multiple projects.

### 2.3 project_members

Stores accepted project memberships.

| Column | Type | Description |
|---|---|---|
| id | BIGINT, Primary Key | Unique membership ID |
| project_id | BIGINT, Foreign Key | Related project |
| user_id | BIGINT, Foreign Key | Accepted team member |
| joined_at | TIMESTAMP, Nullable | Membership acceptance time |
| created_at | TIMESTAMP | Record creation time |
| updated_at | TIMESTAMP | Last update time |

Rules:
- A user can belong to multiple projects.
- A project can have multiple members.
- The same user must not be added to the same project more than once.
- The project owner is identified through the projects table.

### 2.4 project_invitations

Stores invitations sent to users to join projects.

| Column | Type | Description |
|---|---|---|
| id | BIGINT, Primary Key | Unique invitation ID |
| project_id | BIGINT, Foreign Key | Invited project |
| invited_by | BIGINT, Foreign Key | User who sent the invitation |
| invited_user_id | BIGINT, Foreign Key | Registered user being invited |
| email | VARCHAR | Invitation email address |
| status | VARCHAR | Pending, Accepted, or Rejected |
| responded_at | TIMESTAMP, Nullable | Response date and time |
| created_at | TIMESTAMP | Record creation time |
| updated_at | TIMESTAMP | Last update time |

Rules:
- Invitations are associated with a project and an intended recipient.
- Only the invited user can accept or reject the invitation.
- Accepted invitations create project membership.
- Pending and rejected invitations do not grant membership.

Initial implementation assumption: invitations will be sent to registered users. Inviting users who do not yet have an account can be considered later.

### 2.5 tasks

Stores personal tasks and project tasks.

| Column | Type | Description |
|---|---|---|
| id | BIGINT, Primary Key | Unique task ID |
| user_id | BIGINT, Foreign Key | User who created the task |
| project_id | BIGINT, Nullable Foreign Key | Related project; null for personal tasks |
| assigned_to | BIGINT, Nullable Foreign Key | User assigned to the task |
| title | VARCHAR | Task title |
| description | TEXT, Nullable | Task details |
| due_date | DATE, Nullable | Task deadline |
| priority | VARCHAR | Low, Medium, or High |
| status | VARCHAR | To Do, In Progress, or Completed |
| created_at | TIMESTAMP | Record creation time |
| updated_at | TIMESTAMP | Last update time |

Rules:
- A task with no project is a personal task.
- A project task must belong to a valid project.
- Assigned users must be authorized to work on the project.
- The task creator and assigned user may be different.
- Task access and modification must be controlled through authorization checks.

## 3. Database Relationships

- User has many Projects through `projects.owner_id`.
- Project belongs to one owner through `projects.owner_id`.
- Project has many Tasks through `tasks.project_id`.
- User has many Tasks created through `tasks.user_id`.
- User has many Tasks assigned through `tasks.assigned_to`.
- Project belongs to many Users through `project_members`.
- Project has many Invitations through `project_invitations.project_id`.
- User can receive many Invitations through `project_invitations.invited_user_id`.
- User can send many Invitations through `project_invitations.invited_by`.

## 4. Data Integrity

- Use foreign keys to maintain relationships.
- Use unique constraints to prevent duplicate project memberships.
- Use validation for status, priority, and date fields.
- Protect records from unauthorized access.
- Define appropriate deletion behavior for related records.

## 5. Planned Database Tables

1. users
2. projects
3. project_members
4. project_invitations
5. tasks

## 6. Future Improvements

Possible future additions include task comments, attachments, notifications, activity logs, and project progress tracking.
