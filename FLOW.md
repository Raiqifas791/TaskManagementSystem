# FLOW.md — Task Management System

## 1. Application Overview

This document describes the main workflows of the Task Management System built with Laravel and Blade.

The application allows users to manage personal tasks, create multiple projects, invite team members, and collaborate on project tasks.

## 2. User Registration and Login Flow

1. The user opens the application.
2. The user registers with name, email, and password.
3. The system validates the submitted information.
4. The system creates the user account.
5. The user logs in using their credentials.
6. After successful authentication, the user accesses the dashboard.

## 3. Project Creation Flow

1. The authenticated user opens My Projects.
2. The user clicks Create Project.
3. The user enters the project name and optional details.
4. The system validates the information.
5. The system saves the project with the current user as its owner.
6. The project appears in the user's project list.
7. The owner can open the project details page.

## 4. Team Invitation Flow

1. The project owner opens a project.
2. The owner enters the email address of a registered user.
3. The system verifies that the owner has permission to invite members.
4. The system checks that the recipient is eligible to join and is not already a member.
5. The system creates an invitation with Pending status.
6. The recipient receives an invitation notification by email.
7. The recipient opens Team Invitations.
8. The recipient can accept or reject the invitation.

### If the Invitation Is Accepted

1. The system verifies that the invitation belongs to the recipient.
2. The invitation status changes to Accepted.
3. The system adds the recipient to the project's membership records.
4. The user can access the project as an accepted member.

### If the Invitation Is Rejected

1. The system verifies that the invitation belongs to the recipient.
2. The invitation status changes to Rejected.
3. No project membership is created.
4. The recipient does not gain access to the project as a member.

## 5. Personal Task Flow

1. The user opens My Tasks.
2. The user clicks Create Task.
3. The user enters the task title and optional description, due date, and priority.
4. The user selects or confirms the task as a personal task.
5. The system validates and saves the task without a project ID.
6. The task appears in the user's task list.
7. The user can update its status or edit the task according to permissions.

## 6. Project Task Flow

1. An authorized project owner or member opens a project.
2. The user opens the project's task section.
3. The user clicks Create Task.
4. The user enters the task details.
5. The user selects a project member as the assignee, if required.
6. The system validates the project and assignee permissions.
7. The system saves the task under the selected project.
8. The task appears in the project's task list.
9. The assigned user can view and update the task according to permissions.

## 7. Task Status Flow

A task follows these statuses:

**To Do → In Progress → Completed**

- To Do: The task has not been started.
- In Progress: Work on the task is underway.
- Completed: The task has been finished.

Authorized users can update task status as work progresses.

## 8. Dashboard Flow

1. The user logs in.
2. The dashboard loads the user's authorized project and task information.
3. The dashboard displays relevant project and task summaries.
4. The user can navigate to My Projects, My Tasks, Team Invitations, or Profile.
5. All displayed data must respect user permissions.

## 9. Authorization Flow

Whenever a user requests a protected action:

1. The system checks whether the user is authenticated.
2. The system retrieves the requested resource.
3. The system checks the user's ownership, membership, or other applicable permissions.
4. If authorized, the system performs the action.
5. If unauthorized, the system denies access and returns an appropriate response.

## 10. Main Application Workflow

User Registration/Login  
↓  
Dashboard  
↓  
Create or View Projects  
↓  
Invite Team Members  
↓  
Invitation Pending  
↓  
Accept or Reject Invitation  
↓  
Accepted Members Access the Project  
↓  
Create and Assign Project Tasks  
↓  
Update Task Status  
↓  
Track Project and Task Progress

Personal tasks can also be created and managed independently of projects.

## 11. Important Implementation Notes

- Email delivery must be configured for real invitation emails.
- Invitation responses must be restricted to the intended recipient.
- Project access must be checked on the server.
- Task assignments must be limited to eligible project members.
- Database transactions should be used where needed to keep invitation acceptance and membership creation consistent.
- The application must validate all user-submitted data.
