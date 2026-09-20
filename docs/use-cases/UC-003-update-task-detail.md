# Use Case: UC-003 Update Task Detail

## Overview
**Use Case ID:** UC-003
**Use Case Name:** Update Task Detail
**Primary Actor:** User
**Goal:** Update the description and/or due date of an existing task
**Status:** Draft

## Linked Requirements
FR-003, C-001

## Preconditions
- The actor is authenticated.
- The task exists.
- The task status is not DELETED.

## Trigger
- The actor selects "Edit Task" on a task.

## Main Success Scenario
1. The actor opens the task edit form.
2. The system displays the task's current description and due date.
3. The actor modifies the description and/or the due date.
4. The system validates that the description is not empty.
5. The system validates that the due date, if provided, is today or a future date.
6. The system saves the updated task details.
7. The system records an UPDATED entry in the task history.
8. The system confirms the update.

## Alternative Flows

### A1: Description is empty
**Trigger:** At step 4, the description is empty.
1. The system informs the actor that a description is required.
2. The system does not save the changes.
3. The use case ends without updating the task.

### A2: Due date is in the past
**Trigger:** At step 5, the due date is earlier than today.
1. The system informs the actor that the due date must be today or later.
2. The system does not save the changes.
3. The use case ends without updating the task.

## Exception Flows

### E1: Database unavailable
**Trigger:** At step 6, the database is unreachable.
1. The system logs the error and informs the actor.
2. The task remains unchanged.

### E2: Task is DELETED
**Trigger:** At step 1, the task status is DELETED.
1. The system informs the actor that a deleted task cannot be edited.
2. The use case ends without opening the edit form.

## Postconditions
**Success:**
- The task's description and/or due date reflect the new values.
- An UPDATED entry exists in the task history for the task.

**Failure:**
- The task remains unchanged.

## Business Rules
- **BR-003-1:** A task description must not be empty.
- **BR-003-2:** A task's due date, if provided, must be today or a future date.
- **BR-003-3:** A task with status DELETED cannot be updated.

## Traceability Metadata
```yaml
id: UC-003
name: Update Task Detail
actors: [User]
linkedRequirements: [FR-003, C-001]
entities: [Task, TaskHistory]
postconditions:
  - Task description/dueDate updated
  - TaskHistory UPDATED entry recorded
```
