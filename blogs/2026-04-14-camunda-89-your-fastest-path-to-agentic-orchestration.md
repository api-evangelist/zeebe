---
title: "Camunda 8.9: Your Fastest Path to Agentic Orchestration"
url: "https://camunda.com/blog/2026/04/camunda-8-9-fastest-path-to-agentic-orchestration/"
date: "Tue, 14 Apr 2026 14:06:45 +0000"
author: "Amy Johnston"
feed_url: "https://camunda.com/feed/"
---
<p id="h.q4vwsseoq8zw">AI is advancing quickly and enterprises are deploying agents faster than ever. But end-to-end business processes—the complete insurance claim journey, the full order-to-cash cycle, the mortgage that moves from application to approval—require an orchestration layer that coordinates AI agents, knowledge workers, and tools and systems with the governance and control that mission-critical operations demand.</p>



<p>Camunda 8 is that orchestration layer. It blends support for deterministic process logic with <a href="https://camunda.com/enterprise-grade-agents/" target="_blank">enterprise-grade agents</a>&nbsp;that you can trust at scale. Adopting Camunda 8 paves the way for agentic orchestration that coordinates people, systems, and AI agents across end-to-end business processes with the governance and control that mission-critical operations demand.</p>



<h2 class="wp-block-heading" id="h.35uqjtfn9uhu">Combine the best of deterministic and dynamic orchestration</h2>



<p>Business processes are often built on deterministic logic for good reason: clear sequencing, predictable outcomes, and a reliable audit trail. But even the most well-designed process encounters conditions that couldn’t be fully anticipated at design time; for example, a customer’s circumstances change mid-application, an AI agent surfaces an anomaly, or a regulatory condition shifts the required path.</p>



<p><a href="https://docs.camunda.io/docs/next/components/modeler/bpmn/conditional-events/" target="_blank">BPMN conditional events</a>&nbsp;extend that deterministic foundation to handle these moments. When an AI agent produces an assessment, a conclusion, or a decision, the process can act on it immediately: interrupting the current path, redirecting to a new one, or escalating based on what the agent determined. The process remains structured and auditable; it simply has the flexibility to respond to what emerges during execution.</p>



<p>The result is automation that handles the expected with precision, and the unexpected with the same level of control.</p>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image1" class="wp-image-162543" height="932" src="https://camunda.com/wp-content/uploads/2026/04/image1-2-1.png" width="1999" /></figure>
</div>


<h2 class="wp-block-heading" id="h.9hu64dzbp65x">Accelerate Camunda adoption&nbsp;with more database options</h2>



<p>To achieve success with AI agents, you need to fully integrate them into your business processes. The same goes for your tech stack; operations teams need an agentic orchestration platform that they can install, integrate, operate, and govern using the tools and practices they’ve already defined. For teams with well-established operations around relational databases, such as backup procedures and monitoring tools, the 8.9 release makes adoption of Camunda easy. </p>



<p>Camunda 8 uses a layered storage model:</p>



<ul class="wp-block-list">
<li>Primary storage for running process execution data</li>



<li>Secondary storage for data used by web applications and APIs</li>
</ul>



<p>This release introduces <a href="https://docs.camunda.io/docs/next/self-managed/concepts/databases/relational-db/rdbms-setup-guide/" target="_blank">support for relational databases</a>&nbsp;as an alternative secondary storage option, in addition to Elasticsearch or OpenSearch. You can now store and query process data in PostgreSQL, Oracle, MariaDB, MySQL, Microsoft SQL Server, Amazon Aurora, or H2.</p>



<p>The Zeebe workflow engine continues to use the proven <a href="https://docs.camunda.io/docs/self-managed/components/orchestration-cluster/zeebe/operations/resource-planning/#rocksdb" target="_blank">RocksDB</a>&nbsp;for primary storage and uses the <a href="https://docs.camunda.io/docs/components/zeebe/technical-concepts/clustering/#raft-consensus-and-replication-protocol" target="_blank">raft protocol</a>&nbsp;to ensure fault tolerance, so you’ll benefit from state persistence for long-running processes and safe recovery in the case of failure.</p>



<p>In addition, <a href="https://docs.camunda.io/docs/self-managed/components/modeler/web-modeler/configuration/#database" target="_blank">Web Modeler</a>&nbsp;now supports MariaDB, MySQL, and H2 in addition to previous support for PostgreSQL and Oracle, aligning its configuration with the Camunda Orchestration Cluster and simplifying Camunda 8 Self-Managed deployments.</p>



<p id="h.ww94wjkoahdc">The enterprises that are best positioned to deploy AI agents at scale are the ones that can adopt an agentic orchestration platform without restructuring the foundational infrastructure layer. Relational database support means teams can run Camunda 8 on the stack they already know and govern. </p>



<h2 class="wp-block-heading" id="h.ww94wjkoahdc">Enforce governance and SLAs across every human task, automatically</h2>



<p>While the use of AI agents is growing, humans are still an important part of everyday business processes with people working alongside agents to deliver better customer experiences without increasing manual workloads. In Camunda, task listeners are an important part of human work, enabling processes to react to the actions that people take. However, it isn’t feasible or scalable for process designers to remember to attach a listener to every user task they put in a process during design time.</p>



<p>Camunda 8.9 introduces <a href="https://docs.camunda.io/docs/next/components/concepts/global-user-task-listeners/" target="_blank">global user task listeners</a>&nbsp;that enable all processes to react to user task lifecycle events. You configure listeners at the cluster level, meaning they will be applied across the entire cluster as soon as it starts up. One configuration, applied everywhere, enforced structurally—not dependent on whether a process designer remembered to attach a listener to a task when they built the process.</p>



<p>Global task listeners are particularly useful for:</p>



<ul class="wp-block-list">
<li>Enforcing governance rules and validations</li>



<li>Centralizing SLAs and notifications across all processes</li>



<li>Consistently applying due date and priority policies</li>
</ul>



<p>As AI agents take on operational responsibilities such as triaging incoming cases, drafting initial assessments, routing tasks to the appropriate team, and requesting approvals, the user tasks that remain in the process are high stakes: an exception that a senior staff member must review, a credit decision requiring documented justification, a regulatory approval with a mandatory audit trail. These are the tasks where a missing listener is not a maintenance inconvenience; it’s a compliance failure.</p>



<p>Global user task listeners ensure the governance layer applied to human-agent collaboration is consistent, auditable, and enforced from the platform level. It’s an architectural approach that makes it safe to give agents real operational authority because the process guarantees every human touchpoint, regardless of how the process is modeled or who built it, inherits the same behavioral standards.</p>



<h2 class="wp-block-heading" id="h.m6nlemrjdmbk">Access a complete, on-demand audit trail for <em>every</em>&nbsp;critical action</h2>



<p>As AI agents take on operational tasks and humans handle the high-stakes exceptions, organizations need a clear, tamper-proof record of who did what, when, and why. Camunda 8.9 introduces a <a href="https://docs.camunda.io/docs/next/components/audit-log/overview/" target="_blank">centralized audit log</a>, available on demand, that captures all critical user and client operations across process, identity, and user task domains.</p>



<ul class="wp-block-list">
<li><strong>Compliance teams </strong>can query the log to produce defensible evidence during internal and external audits</li>



<li><strong>Operations teams </strong>can trace the sequence of actions that led to a problem in a process or decision</li>



<li><strong>Security teams </strong>can investigate identity changes and detect potential unauthorized access</li>



<li><strong>Administrators</strong>&nbsp;can verify that governance controls were followed throughout</li>
</ul>



<p>Audit entries are available through <a href="https://docs.camunda.io/docs/next/apis-tools/orchestration-cluster-api-rest/specifications/search-audit-logs/" target="_blank">Orchestration Cluster API</a>&nbsp;and integrated into Operate, Tasklist, and Identity, with role-based access controls to ensure only authorized personnel can view sensitive audit data. You can also configure which actor types, operation categories, and granular operations are captured, so audit collection aligns with your compliance policies without unnecessary data volume.</p>



<h2 class="wp-block-heading" id="h.2kpqm6rpbmfb">Connect AI agents to your running cluster</h2>



<p>Building AI-powered applications that work with Camunda has traditionally required custom client code: REST API calls, authentication handling, response parsing, and data formatting for AI consumption. Camunda 8.9 removes that work entirely. The <a href="https://docs.camunda.io/docs/next/apis-tools/orchestration-cluster-api-mcp/orchestration-cluster-api-mcp-overview/">Orchestration Cluster MCP Server</a> exposes Camunda&#8217;s operational capabilities through the Model Context Protocol (MCP), a standardized interface that any MCP-compliant AI agent or application can use to discover and invoke Camunda tools without bespoke integration code. Claude Code, VS Code with GitHub Copilot, Cursor, and custom AI applications can all connect to a running cluster and interact with it directly.</p>



<p>The available tools cover the full operational surface: checking cluster health, searching and resolving incidents, querying process definitions and instances, managing user tasks, and retrieving variables. An AI agent can ask what&#8217;s running in a cluster, locate a stalled instance, understand the failure, and resolve the incident, all without dashboard navigation or log parsing. For operations teams, it turns a running Camunda cluster into something you can simply talk to.</p>



<p>The MCP server is enabled by default in Camunda 8 Run for local development, and can be <a href="https://docs.camunda.io/docs/next/apis-tools/orchestration-cluster-api-mcp/orchestration-cluster-api-mcp-setup/">explicitly enabled</a> for production deployments. It shares the same authentication and authorization model as the <a href="https://docs.camunda.io/docs/next/apis-tools/orchestration-cluster-api-rest/specifications/search-audit-logs/">Orchestration Cluster REST API</a>, so there&#8217;s no separate security configuration to manage.</p>



<h2 class="wp-block-heading" id="h.2kpqm6rpbmfb">Enable multi-agent communication through A2A</h2>



<p>Multi-agent automation is becoming a practical reality, and the Camunda 8.9 release adds dedicated support for the Agent2Agent (A2A) protocol, an open standard that enables AI agents from different providers and domains to communicate and coordinate through signed, structured messages. In a loan origination process, for example, a credit assessment agent can request a fraud risk score from a specialist fraud detection agent mid-process and receive a structured response before continuing—without any custom integration work between the two.</p>



<p>With three dedicated connectors, you have the flexibility to implement A2A in the way that fits your process design. You can also expose A2A agents as tools inside a Camunda agent, enabling it to select the right specialist dynamically based on context; so an HR onboarding agent, for instance, can invoke a security and access agent to determine the right permissions profile for a new hire before provisioning proceeds. In all cases, Camunda maintains the audit trail, enforces governance guardrails, and keeps agent interactions inside a governed process model where you control the entry and exit criteria, boundaries, and escalation paths.</p>



<p>For a deep dive into implementation patterns and a real-world mortgage lending example, read our two-part series:</p>



<ul class="wp-block-list">
<li><a href="https://camunda.com/blog/2026/02/using-a2a-to-achieve-your-business-goals-pt-1/" target="_blank">Designing A2A Orchestration with Camunda: The Foundation</a></li>



<li><a href="https://camunda.com/blog/2026/02/using-a2a-to-achieve-your-business-goals-pt-2/" target="_blank">Delivering A2A Orchestration with Camunda: A Practical Example</a></li>
</ul>



<h2 class="wp-block-heading" id="h.pvtnbqfkpjt6">Migrate AI agents without disrupting running business processes</h2>



<p>One of the defining characteristics of agentic processes is that they change. You fine-tune LLM prompts, integrate new tools, add human guardrails, and introduce new A2A or MCP agents as your automation matures. But when you deploy an updated process definition, there may be thousands of instances already running in production, mid-execution, carrying real business data.</p>



<p>With Camunda 8.9, process instance migration supports <a href="https://docs.camunda.io/docs/components/connectors/out-of-the-box-connectors/agentic-ai-aiagent-subprocess/" target="_blank">ad-hoc sub-processes</a>, the BPMN construct at the heart of dynamic agent behavior. You can move in-flight process instances from one version of a process model to an updated one, preserving execution state, variables, and business progress across versions. There&#8217;s no need to cancel and restart live work to take advantage of improved logic; the migration moves your instances forward, with traceability intact.</p>



<p>This is the foundation of business continuity for agentic operations. For teams actively iterating on agentic processes in production, the ability to upgrade agent behavior safely and systematically—without interrupting the work already in motion—is as important as the automation itself.</p>



<p>For more on how process instance migration works and why it matters as a strategic capability, read <a href="https://camunda.com/blog/2026/01/migrate-your-agentic-processes-without-disruption-using-process-instance-migration/" target="_blank">Migrate Your Agentic Processes Without Disruption Using Process Instance Migration</a>.</p>



<h2 class="wp-block-heading" id="h.m5i764xu9e08">What comes next</h2>



<p>To learn more about Camunda 8.9 and get a sneak peek of the future of agentic coding with Camunda, join us on May 6th at 10 AM EDT / 4 PM CEST for the webinar: <em><a href="https://page.camunda.com/wb-stronger-foundations-smarter-processes-camunda" target="_blank">Stronger Foundations, Smarter Processes: Camunda 8.9 Unlocks Enterprise-Grade Agentic Orchestration</a></em>. </p>



<p>And there’s still time to join us at <a href="https://www.camundacon.com/" target="_blank">CamundaCon 2026</a>, happening May 19-21 in Amsterdam. Register today!</p>



<div class="wp-block-buttons is-layout-flex wp-block-buttons-is-layout-flex">
<div class="wp-block-button"><a class="wp-block-button__link wp-element-button" href="https://www.camundacon.com/">Register for CamundaCon</a></div>
</div>



<p></p>
<p>The post <a href="https://camunda.com/blog/2026/04/camunda-8-9-fastest-path-to-agentic-orchestration/">Camunda 8.9: Your Fastest Path to Agentic Orchestration</a> appeared first on <a href="https://camunda.com">Camunda</a>.</p>
