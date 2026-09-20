# Use Case: UC-005 View Task History

## Overview
**Use Case ID:** UC-005
**Use Case Name:** View Task History
**Primary Actor:** User
**Goal:** View the history of changes made to a task
**Status:** Draft

## Linked Requirements
FR-005

## Preconditions
- The actor is authenticated.
- The task exists.

## Trigger
- The actor selects "View History" on a task.

## Main Success Scenario
1. The actor opens the task detail page.
2. The actor selects "View History".
3. The system retrieves the task's history entries ordered from most recent to oldest.
4. The system displays each history entry with its change type, the user who made the change, and the timestamp.

## Alternative Flows

### A1: No history entries exist
**Trigger:** At step 3, the task has no history entries.
1. The system displays a message that no history exists for this task.
2. The use case ends.

## Exception Flows

### E1: Database unavailable
**Trigger:** At step 3, the database is unreachable.
1. The system informs the actor that the task history is unavailable.
2. No history entries are displayed.

## Postconditions
**Success:**
- The task's history entries are displayed to the actor.

**Failure:**
- No history entries are displayed; the actor is informed of the unavailability.

## Business Rules
- **BR-005-1:** History entries are read-only and cannot be edited or deleted by the actor.
- **BR-005-2:** History entries are displayed ordered from most recent to oldest.

## Traceability Metadata
```yaml
id: UC-005
name: View Task History
actors: [User]
linkedRequirements: [FR-005]
entities: [Task, TaskHistory]
postconditions:
  - TaskHistory entries displayed to actor
```
