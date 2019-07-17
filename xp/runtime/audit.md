# Audit Log

## Specifications

### Specs validated.
- Applications must be able to use audit logs.
- Core Services (except NodeService or services used by NodeService) must be able to use audit logs.
- A JS library must wrap the Audit Log Service and expose its capabilities

### Additional propositions
- Audit Log API users must be able to store audit logs.
- Audit Log API users must be able to retrieve/query audit logs.
- Audit Log API users must be able to be notified on audit log storage
- Audit Log is configurable

### Problematics remaining

- Handle fact that this data will keep growing in size. 
  - Solution1: Split it into different repositories based on time

## Data

- AuditLog
  - id: AuditLogId // == NodeId OR RepositoryId+NodeId
  - type: String
  - level: AuditLogLevel
  - timestamp: Instant
  - bundleName: String //Alternative "applicationKey: ApplicationKey"
  - user: PrincipalKey
  - labels: String[]
  - message: String //Alternative naming "action" or "description"
  - data: String //Optional, Unstructured JSON

## API
- AuditLogService
  - log(LogAuditLogParams): AuditLog
  - get(AuditLogId): AuditLog
  - delete(AuditLogIds): AuditLog
  - query(QueryAuditLogParams): QueryAuditLogResult

- QueryAuditLogResult
  - total: long
  - hits: AuditLogs
  
## Event

- Event type: "audit.log"
- Event data:
  - id // Serialized AuditLogId
  
