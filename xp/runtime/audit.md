# Audit Log

## Specifications

### Specs validated.
- Applications must be able to use audit logs.
- Core Services (except NodeService or services used by NodeService) must be able to use audit logs.
- A JS library must wrap the Audit Log Service and expose its capabilities
- Audit Log API users must be able to store audit logs.
- Audit Log API users must be able to retrieve/query audit logs.
- Audit Log API users must be able to be notified on audit log storage (Not in version 1)
- Audit Log is configurable (Not in version 1)
  - Audit Log can be disabled or not
  - Audit Log data will be vacuumed automatically

## Data

- Repository name: system.auditlog
- AuditLog
  - id: AuditLogId // == NodeId OR RepositoryId+NodeId
  - type: String
  - level: AuditLogLevel
  - logTime: Instant
  - source: String //Alternative "applicationKey: ApplicationKey"
  - user: PrincipalKey
  - labels: String[]
  - data: PropertyTree

## API
- AuditLogService
  - log(LogAuditLogParams): AuditLog
  - get(AuditLogId): AuditLog
  - delete(AuditLogIds): AuditLog
  - query(QueryAuditLogParams): QueryAuditLogResult

- QueryAuditLogResult
  - total: long
  - hits: AuditLogs

  
