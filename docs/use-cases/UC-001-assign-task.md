# Use Case: UC-001 Assign Task

## Overview
**Use Case ID:** UC-001
**Use Case Name:** Assign Task
**Primary Actor:** User
**Goal:** Assign an open task to another active user
**Status:** Draft

## Linked Requirements
FR-001, NFR-001, C-001

## Preconditions
- The actor is authenticated.
- The task exists.
- The task is open and not yet assigned.

## Trigger
- The actor selects "Assign Task" on a task.

## Main Success Scenario
1. The actor opens the task details.
2. The system displays the task details and a list of active users.
3. The actor selects a target user.
4. The system validates that the selected user is active.
5. The system assigns the task to the selected user.
6. The system confirms the assignment.

## Alternative Flows

### A1: Selected user is inactive
**Trigger:** At step 4, the selected user is inactive.
1. The system informs the actor that the selected user cannot receive tasks because the user is not active.
2. The system does not assign the task.
3. The use case ends without changes to the task assignment.

## Exception Flows

### E1: Database unavailable
**Trigger:** At step 5, the database is unreachable.
1. The system logs the error and informs the actor.
2. The task remains unchanged.

## Postconditions
**Success:**
- The task is assigned to the selected active user.
- The task status is ASSIGNED.

**Failure:**
- The task assignment remains unchanged.

## Business Rules
- **BR-001-1:** Only active users can receive task assignments.
- **BR-001-2:** An assigned task must have exactly one assignee.

## Traceability Metadata
```yaml
id: UC-001
name: Assign Task
actors: [User]
linkedRequirements: [FR-001, NFR-001, C-001]
entities: [User, Task]
postconditions:
  - Task assigned to target user
```
