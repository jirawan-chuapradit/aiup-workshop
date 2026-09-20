# Use Case: UC-002 Create Task

## Overview
**Use Case ID:** UC-002
**Use Case Name:** Create Task
**Primary Actor:** User
**Goal:** Create a new task
**Status:** Draft

## Linked Requirements
FR-002, C-001

## Preconditions
- The actor is authenticated.

## Trigger
- The actor selects "Create Task".

## Main Success Scenario
1. The actor opens the create task form.
2. The actor enters a task description and, optionally, a due date.
3. The system validates that the description is not empty.
4. The system validates that the due date, if provided, is today or a future date.
5. The system creates the task with status OPEN.
6. The system records a CREATED entry in the task history.
7. The system confirms the creation and displays the new task.

## Alternative Flows

### A1: Description is empty
**Trigger:** At step 3, the description is empty.
1. The system informs the actor that a description is required.
2. The system does not create the task.
3. The use case ends without creating a task.

### A2: Due date is in the past
**Trigger:** At step 4, the due date is earlier than today.
1. The system informs the actor that the due date must be today or later.
2. The system does not create the task.
3. The use case ends without creating a task.

## Exception Flows

### E1: Database unavailable
**Trigger:** At step 5, the database is unreachable.
1. The system logs the error and informs the actor.
2. No task is created.

## Postconditions
**Success:**
- A new task exists with status OPEN.
- A CREATED entry exists in the task history for the new task.

**Failure:**
- No task is created.

## Business Rules
- **BR-002-1:** A task description must not be empty.
- **BR-002-2:** A task's due date, if provided, must be today or a future date.
- **BR-002-3:** A newly created task's status is always OPEN.

## Traceability Metadata
```yaml
id: UC-002
name: Create Task
actors: [User]
linkedRequirements: [FR-002, C-001]
entities: [Task, TaskHistory]
postconditions:
  - Task created with status OPEN
  - TaskHistory CREATED entry recorded
```
