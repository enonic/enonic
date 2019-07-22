# Audit Log

## Specifications

### Specs validated.
- Applications must be able to use audit logs.
- Core Services (except NodeService or services used by NodeService) must be able to use audit logs.
- A JS library must wrap the Audit Log Service and expose its capabilities
- Audit Log API users must be able to store audit logs.
- Audit Log API users must be able to retrieve/query audit logs.
- Audit Log API users must be able to be notified on audit log storage (Not in version 1)
- Audit Log is configurable
  - Audit Log can be disabled or not
- Audit Logs should also be logged. (configurable)
- Audit Log data will be vacuumed automatically (Not in version 1)

## Data

- Repository name: system.auditlog
- AuditLog
  - id: AuditLogId // == NodeId
  - type: String
  - time: Instant //Default: Current time
  - source: String //Default: Bundle name
  - user: PrincipalKey //Default: Current User
  - message: String //Default: Empty string
  - object: URI[]
  - data: PropertyTree

## API
- AuditLogService
  - log(LogAuditLogParams): AuditLog
  - get(AuditLogId): AuditLog
  - delete(AuditLogIds): AuditLog
  - find(FindAuditLogParams): FindAuditLogResult

- FindAuditLogResult
  - total: long
  - hits: AuditLogs

  
