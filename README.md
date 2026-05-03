# Zeebe

Zeebe is the cloud-native workflow engine that powers Camunda 8, providing scalable, resilient workflow automation and microservices orchestration without relying on a central database. It implements BPMN 2.0 process execution and enables high throughput with horizontal scaling through a partitioned, replicated architecture.

- **Website:** https://camunda.com/platform/zeebe/
- **Documentation:** https://docs.camunda.io/docs/components/zeebe/zeebe-overview/
- **REST API Docs:** https://docs.camunda.io/docs/apis-tools/zeebe-api-rest/zeebe-api-rest-overview/
- **GitHub:** https://github.com/camunda/camunda

## APIs

| API | Type | Description |
|---|---|---|
| Zeebe REST API | OpenAPI | Process deployment, instance management, job handling, messages, signals, incidents, user tasks |

## OpenAPI Specifications

| Spec | Path |
|---|---|
| Zeebe REST API | [openapi/zeebe-api.yml](openapi/zeebe-api.yml) |

## Artifacts

### Spectral Rules
- [rules/zeebe-rules.yml](rules/zeebe-rules.yml) — Spectral ruleset enforcing Zeebe API conventions

### Naftiko Capabilities

| File | Description |
|---|---|
| [capabilities/process-orchestration.yaml](capabilities/process-orchestration.yaml) | Unified workflow capability for BPMN process orchestration (15 tools) |
| [capabilities/shared/zeebe-api.yaml](capabilities/shared/zeebe-api.yaml) | Shared per-API definition for Zeebe REST API |

### JSON Schema
- [json-schema/zeebe-process-instance-schema.json](json-schema/zeebe-process-instance-schema.json)
- [json-schema/zeebe-job-schema.json](json-schema/zeebe-job-schema.json)

### JSON Structure
- [json-structure/zeebe-process-instance-structure.json](json-structure/zeebe-process-instance-structure.json)
- [json-structure/zeebe-job-structure.json](json-structure/zeebe-job-structure.json)

### JSON-LD
- [json-ld/zeebe-context.jsonld](json-ld/zeebe-context.jsonld) — Linked data context mapping Zeebe types to schema.org and BPMN ontologies

### Examples
- [examples/zeebe-getTopology-example.json](examples/zeebe-getTopology-example.json)
- [examples/zeebe-deployResources-example.json](examples/zeebe-deployResources-example.json)
- [examples/zeebe-createProcessInstance-example.json](examples/zeebe-createProcessInstance-example.json)
- [examples/zeebe-activateJobs-example.json](examples/zeebe-activateJobs-example.json)
- [examples/zeebe-publishMessage-example.json](examples/zeebe-publishMessage-example.json)

### Vocabulary
- [vocabulary/zeebe-vocabulary.yml](vocabulary/zeebe-vocabulary.yml) — Domain vocabulary for Zeebe/Camunda process orchestration

## Key Concepts

- **BPMN** — Business Process Model and Notation; Zeebe executes BPMN 2.0 process definitions
- **Job Workers** — Microservices that poll for and process jobs created by service tasks
- **Message Correlation** — Correlate published messages to waiting process subscriptions via correlation key
- **Horizontal Scaling** — Partitioned architecture enables scaling without a central database
- **Multi-Tenancy** — Logical resource isolation via tenantId across all resources

## Links

- **Forum:** https://forum.camunda.io/
- **Community Hub:** https://github.com/camunda-community-hub
- **Postman:** https://www.postman.com/camundateam/camunda-8-postman/collection/j0knqwp/zeebe-api-rest
- **Pricing:** https://camunda.com/pricing/
