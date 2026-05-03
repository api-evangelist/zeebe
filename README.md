# Zeebe (zeebe)
Zeebe is the cloud-native workflow engine that powers Camunda 8, providing scalable, resilient workflow automation and microservices orchestration without relying on a central database, enabling high throughput with horizontal scaling. It implements BPMN 2.0 process execution and provides a REST API for process deployment, instance management, job handling, message correlation, and cluster topology queries.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - BPMN, Camunda, Cloud Native, Distributed Systems, Java, Microservices, Process Automation, Workflow Orchestration

## Timestamps

- **Created:** 2026-03-26
- **Modified:** 2026-05-04

## APIs

### Zeebe REST API
The Zeebe REST API provides programmatic access to the Zeebe workflow engine powering Camunda 8. It enables process deployment, process instance creation and management, job activation and completion, message and signal publishing, incident resolution, user task management, and cluster topology queries.

**Human URL:** [https://docs.camunda.io/docs/apis-tools/zeebe-api-rest/zeebe-api-rest-overview/](https://docs.camunda.io/docs/apis-tools/zeebe-api-rest/zeebe-api-rest-overview/)

#### Tags:

 - BPMN, Camunda, Cloud Native, Microservices, Process Automation, Workflow Orchestration

#### Properties

- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/openapi/zeebe-api.yml)
- [Documentation](https://docs.camunda.io/docs/apis-tools/zeebe-api-rest/zeebe-api-rest-overview/)
- [Postman](https://www.postman.com/camundateam/camunda-8-postman/collection/j0knqwp/zeebe-api-rest)
- [Spectral Rules](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/rules/zeebe-rules.yml)
- [Examples](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/examples/)
- [JSONSchema](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/json-schema/)
- [JSONStructure](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/json-structure/)
- [JSONLD](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/json-ld/zeebe-context.jsonld)
- [Vocabulary](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/vocabulary/zeebe-vocabulary.yml)
- [Capabilities](https://raw.githubusercontent.com/api-evangelist/zeebe/refs/heads/main/capabilities/)

## Common Properties

- [Website](https://camunda.com/platform/zeebe/)
- [Documentation](https://docs.camunda.io/docs/components/zeebe/zeebe-overview/)
- [Documentation](https://docs.camunda.io/docs/apis-tools/zeebe-api-rest/zeebe-api-rest-overview/)
- [Getting Started](https://docs.camunda.io/docs/guides/)
- [GitHub](https://github.com/camunda/camunda)
- [GitHubOrg](https://github.com/camunda)
- [GitHubOrg](https://github.com/camunda-community-hub)
- [Pricing](https://camunda.com/pricing/)
- [Blog](https://camunda.com/blog/)
- [Issues](https://github.com/camunda/camunda/issues)
- [SDK](https://github.com/camunda/camunda-bpm-spring-boot-starter)
- [SDK](https://github.com/camunda-community-hub/zeebe-client-csharp)
- [SDK](https://github.com/camunda-community-hub/micronaut-zeebe-client)
- [ChangeLog](https://github.com/camunda/camunda/releases)
- [Forum](https://forum.camunda.io/)

## Artifacts

Machine-readable API specifications organized by format.

### OpenAPI

- [zeebe-api.yml](openapi/zeebe-api.yml)

### JSON Schema

- [zeebe-api-activate-jobs-request-schema.json](json-schema/zeebe-api-activate-jobs-request-schema.json)
- [zeebe-api-create-process-instance-request-schema.json](json-schema/zeebe-api-create-process-instance-request-schema.json)
- [zeebe-api-deployment-response-schema.json](json-schema/zeebe-api-deployment-response-schema.json)
- [zeebe-api-job-schema.json](json-schema/zeebe-api-job-schema.json)
- [zeebe-api-process-instance-schema.json](json-schema/zeebe-api-process-instance-schema.json)
- [zeebe-api-publish-message-request-schema.json](json-schema/zeebe-api-publish-message-request-schema.json)
- [zeebe-api-topology-response-schema.json](json-schema/zeebe-api-topology-response-schema.json)

### JSON Structure

- [zeebe-api-activate-jobs-request-structure.json](json-structure/zeebe-api-activate-jobs-request-structure.json)
- [zeebe-api-create-process-instance-request-structure.json](json-structure/zeebe-api-create-process-instance-request-structure.json)
- [zeebe-api-deployment-response-structure.json](json-structure/zeebe-api-deployment-response-structure.json)
- [zeebe-api-job-structure.json](json-structure/zeebe-api-job-structure.json)
- [zeebe-api-process-instance-structure.json](json-structure/zeebe-api-process-instance-structure.json)
- [zeebe-api-publish-message-request-structure.json](json-structure/zeebe-api-publish-message-request-structure.json)
- [zeebe-api-topology-response-structure.json](json-structure/zeebe-api-topology-response-structure.json)

### JSON-LD

- [zeebe-api-context.jsonld](json-ld/zeebe-api-context.jsonld)

### Examples

- [zeebe-activateJobs-example.json](examples/zeebe-activateJobs-example.json)
- [zeebe-api-activate-jobs-request-example.json](examples/zeebe-api-activate-jobs-request-example.json)
- [zeebe-api-create-process-instance-request-example.json](examples/zeebe-api-create-process-instance-request-example.json)
- [zeebe-api-deployment-response-example.json](examples/zeebe-api-deployment-response-example.json)
- [zeebe-api-job-example.json](examples/zeebe-api-job-example.json)
- [zeebe-api-process-instance-example.json](examples/zeebe-api-process-instance-example.json)
- [zeebe-api-publish-message-request-example.json](examples/zeebe-api-publish-message-request-example.json)
- [zeebe-api-topology-response-example.json](examples/zeebe-api-topology-response-example.json)
- [zeebe-createProcessInstance-example.json](examples/zeebe-createProcessInstance-example.json)
- [zeebe-deployResources-example.json](examples/zeebe-deployResources-example.json)
- [zeebe-getTopology-example.json](examples/zeebe-getTopology-example.json)
- [zeebe-publishMessage-example.json](examples/zeebe-publishMessage-example.json)

## Capabilities

Naftiko capabilities organized as shared per-API definitions composed into customer-facing workflows.

### Shared Per-API Definitions

- [Zeebe REST API](capabilities/shared/zeebe-api.yaml) — 16 operations

### Workflow Capabilities

| Workflow | APIs Combined | Tools | Persona |
|----------|--------------|-------|---------|
| [Zeebe Process Orchestration](capabilities/process-orchestration.yaml) | 1 | 16 | Developer |
| [Zeebe Workflow](capabilities/zeebe-workflow.yaml) | 1 | 16 | Developer |

## Vocabulary

- [Zeebe Vocabulary](vocabulary/zeebe-vocabulary.yml) — Unified taxonomy mapping 9 resources, 15 actions, 1 workflows, and 1 personas

## Rules

- [zeebe-rules.yml](rules/zeebe-rules.yml) — 18 rules enforcing Zeebe API conventions

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
