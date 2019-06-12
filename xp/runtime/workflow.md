# Workflow (Runtime)

# Requirements

* Add capability to store the workflow state
* Backward compatibility: If "workflowInfo" is missing from storage, return as READY
* On Content creation, set to IN_PROGRESS

# Breakdown

## New fields

```
Create enum com.enonic.xp.content.WorkflowState
  Possible values: IN_PROGRESS, PENDING_APPROVAL, REJECTED, READY
Create enum com.enonic.xp.content.WorkflowCheckState
  Possible values: PENDING, REJECTED, APPROVED
Create class com.enonic.xp.content.WorkflowInfo
  Field "state" of type ContentWorkflowState
  Field "checks" of type ImmutableMap<String, WorkflowCheckState>
    Check that the key is valid (Property.checkName) / Could create specific class instead of String
Add new field "workflowInfo" on Content of type WorkflowInfo
On Content creation, create a WorkflowInfo with state "IN_PROGRESS"
If "workflowInfo" is missing from storage, return as READY 

Adapt translation from/to Node (ContentDataSerializer)
Check that info is stored, updated and retrieved properly
  While using the admin interface (ContentResource)
  While using the library lib-content
Adapt tests
```

