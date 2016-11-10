# Named Tasks

As a developer, I want to create named tasks that can be executed
with parameters.

This is the basis for scheduling of tasks. UI implementation is not part
of this user-story.

## Estimate

2 weeks

## Requirements

* Tasks should be implemented in Javascript.
* Tasks should be deployed inside an application (/tasks/<name>/<name>.js).
* Tasks should have a display-name and optional config schema (/tasks/<name>/<name>.xml).
* Tasks can be executed using TaskService with parameters.
* Tasks can be executed using the lib-task.
* Tasks should report last execution - time and status.
* Tasks can be listed using lib-task and TaskService.

## Dependencies

None

## Acceptance Criteria

* Execution is done using TaskService "anonymous" execution.
* Documentation of lib-task additions.
* Tests should have minimum 80% code-coverage.
