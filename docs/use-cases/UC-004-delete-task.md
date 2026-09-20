# Use Case: UC-004 Delete Task

## Overview
**Use Case ID:** UC-004
**Use Case Name:** Delete Task
**Primary Actor:** User
**Goal:** Remove an obsolete task from active work
**Status:** Draft

## Linked Requirements
FR-004, C-001

## Preconditions
- The actor is authenticated.
- The task exists.
- The task status is not already DELETED.

## Trigger
- The actor selects "Delete Task" on a task.

## Main Success Scenario
1. The actor selects "Delete Task" on a task.
2. The system asks the actor to confirm the deletion.
3. The actor confirms the deletion.
4. The system sets the task status to DELETED.
5. The system records a DELETED entry in the task history.
6. The system confirms that the task was deleted.

## Alternative Flows

### A1: Actor cancels the confirmation
**Trigger:** At step 3, the actor cancels instead of confirming.
1. The use case ends without deleting the task.

## Exception Flows

### E1: Database unavailable
**Trigger:** At step 4, the database is unreachable.
1. The system logs the error and informs the actor.
2. The task remains unchanged.

### E2: Task already DELETED
**Trigger:** At step 1, the task status is already DELETED.
1. The system informs the actor that the task has already been deleted.
2. The use case ends without changes.

## Postconditions
**Success:**
- The task status is DELETED.
- A DELETED entry exists in the task history for the task.

**Failure:**
- The task remains unchanged.

## Business Rules
- **BR-004-1:** Only a task not already DELETED can be deleted.
- **BR-004-2:** Deletion is recorded as a status change (soft delete); the task record and its history are retained.

## Traceability Metadata
```yaml
id: UC-004
name: Delete Task
actors: [User]
linkedRequirements: [FR-004, C-001]
entities: [Task, TaskHistory]
postconditions:
  - Task status set to DELETED
  - TaskHistory DELETED entry recorded
```
