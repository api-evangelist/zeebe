---
title: "The Case for a Central Business Orchestration Layer—Without Recentralizing Your Architecture"
url: "https://camunda.com/blog/2026/04/case-for-a-central-business-orchestration-layer-without-recentralizing-your-architecture/"
date: "Thu, 23 Apr 2026 17:46:05 +0000"
author: "Bernd Ruecker"
feed_url: "https://camunda.com/feed/"
---
<p>Let’s start with a conversation with a customer that’s surprisingly common in my daily work (as chief technologist for Camunda, the enterprise platform for agentic orchestration):</p>



<p><em><strong>CEO:</strong> “We need more control. I want to understand how the business actually runs—end-to-end. Too many customer journeys are broken, and we need to fix that. And on top of everything, we need to figure out how AI fits into our core operations. If we can’t even see how the business operates today, how can we steer it tomorrow? We need less chaos and more adaptability—otherwise we’ll be out of the market sooner than we think.”</em></p>



<p><em><strong>Me:</strong> “I hear this a lot. What you&#8217;re really asking for is a business orchestration platform: one logical place to understand, coordinate, and steer your core end-to-end processes. Today, that shows up in your architecture as a logically central orchestration layer that ties together different systems, humans, automation tools, bots, and now increasingly AI agents. Because it’s the business processes—not the individual services—that need to evolve fastest.”</em></p>



<p><em><strong>Chief Architect (leaning back, arms crossed):</strong> “Wait a second. Central? Again? That sounds like the old integration-hub era. ESBs, big-box BPM suites… We spent a decade digging ourselves out of those traps. That’s exactly why we went all-in on agile, microservices, and event-driven architectures.”</em></p>



<p><em><strong>CEO (to the architect):</strong></em><em>&nbsp;“I get that. But look at where we are. The chaos seems worse than ever. And nothing changes in reasonable time anymore. Ask five teams how an order flows through our landscape, and you get six different answers.”</em></p>



<p><em><strong>Principal Engineer (half joking, half exhausted):</strong></em><em>&nbsp;“And all of them are partly wrong.”</em></p>



<p><em><strong>Me:</strong> “Exactly. Microservices brought flexibility but also accidental complexity. We introduced distributed-systems headaches, and those so-called decoupled event-driven flows ended up hiding a giant, implicit coordination layer. That invisible layer defines your end-to-end processes…but nobody can see it, measure it, or adapt it. And without understanding your processes, you can’t change anything—let alone introduce AI in a meaningful way. That’s why you need a business orchestration layer.”</em></p>



<p><em><strong>CEO:</strong></em><em>&nbsp;“So you’re suggesting we centralize again?”</em></p>



<p><em><strong>Me:</strong> “Logically central—yes. But operationally and organizationally decentralized. The whole point is <strong>not</strong> to repeat the old patterns. We want clarity and control without slipping back into the same centralizing traps. Let me walk you through what that actually looks like…”</em></p>



<h2 class="wp-block-heading" id="h.2klc4clxyqrm">The architecture pendulum and why the sweet spot is in the middle</h2>



<p>Over the last decade, we’ve been riding a cycle of centralize → decentralize → recentralize—usually as a reaction to past pain rather than thoughtful design. The uncomfortable truth: the sweet spot isn’t at either extreme. It’s right in the middle, where we intentionally balance federation and coordination.</p>



<p>This post explores that balance through the lens of the <strong>business orchestration layer</strong>:</p>



<ul class="wp-block-list">
<li>A logical place where end-to-end processes live</li>



<li>Providing transparency, reliability, and adaptability</li>



<li>Offering a shared understanding of who does what, when, and why</li>
</ul>



<p>At the same time, teams still need autonomy, independent deployability, and the ability to deliver without waiting for a central authority.</p>



<p>The key point: <strong>you can have both</strong> a logically central orchestration layer and a decentralized way of building and operating solutions.</p>



<h2 class="wp-block-heading" id="h.w14q2zta6br6">The problem: end-to-end processes span everything</h2>



<p>From a developer’s perspective, microservices are great—until you try to understand what the business is doing across all those services. But this is exactly where end-to-end processes live: they span organizational, domain, and system boundaries to fulfill a customer goal.</p>



<ul class="wp-block-list">
<li><strong>Place an order at a retailer?<br /></strong>Payments, inventory reservation, warehouse allocation, shipment creation, notifications… Each one handled by a different system.</li>



<li><strong>Open a bank account?<br /></strong>Identity verification, compliance checks, approvals, issuing account numbers, provisioning cards, sending credentials.</li>



<li><strong>File an insurance claim?<br /></strong>Intake, triage, fraud checks, adjuster assignment, document verification, settlement computations, payout.</li>
</ul>



<p>I&#8217;m talking about operational processes here, the ones that run your business every day, span multiple systems, and can&#8217;t just be rebuilt from scratch for every run. The components behind each step might be microservices, SaaS products, on-prem systems, RPA bots, or decades-old legacy software. And within that heterogeneous mess, the end-to-end process still has to happen.</p>



<p>Very often, this happens through point-to-point APIs, brittle integrations, old batch jobs, ESB routes, “serverless glue” scripts, or modern distributed choreography. Those together usually behave like a flash mob—impressive from the outside, unpredictable from within.</p>



<p>After a while, teams start asking for:</p>



<ul class="wp-block-list">
<li>A clear picture of long-running business flows</li>



<li>A common language to discuss processes with business stakeholders</li>



<li>A way to change orchestration logic without touching twenty different components</li>



<li>Insight into where AI should sit and how it should make decisions safely</li>
</ul>



<p>Microservices gave every team autonomy over its domain. But no one got autonomy over the <strong>whole flow</strong>, the journey the customer actually experiences. So end-to-end, the customer journey still depends on manual handoffs and stitched-together integrations. Customers hit what I call the <strong>automation ceiling</strong>: AI and automation capabilities are there, but without orchestration, they don&#8217;t translate into reliable end-to-end outcomes.</p>



<h2 class="wp-block-heading" id="h.67rgpudqlm7y"><strong>SOA and microservices: dead-ends we’ve already lived through</strong></h2>



<p>Historically, service oriented architecture (SOA) tried to solve this by introducing the Enterprise Service Bus (ESB). I was around when ESBs promised transformation, routing, integration, process logic, and governance. The ESB, however, had a very technical focus and created bottlenecks instead of business agility.</p>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image2" class="wp-image-162814" height="422" src="https://camunda.com/wp-content/uploads/2026/04/image2-4-1.png" width="731" /></figure>
</div>


<p><em>A typical ESB vision from the past (taken from </em><em><a href="https://www.tutorialspoint.com/soa/soa_enterprise_service_bus.htm" target="_blank">https://www.tutorialspoint.com/soa/soa_enterprise_service_bus.htm</a></em><em>) </em></p>



<p>The problem was not the idea of orchestration; the problem was <strong>how</strong> ESBs implemented it:</p>



<ul class="wp-block-list">
<li><strong>Centralized ownership</strong> → one team became the gatekeeper for every change</li>



<li><strong>Centralized runtime</strong> → a single box that became the critical path</li>



<li><strong>Implicit coupling</strong> → the ESB rewired APIs on your behalf</li>



<li><strong>Hidden logic</strong> → flows buried in scripts and proprietary config</li>



<li><strong>No developer lifecycle</strong> → no versioning, testing, or CI/CD</li>
</ul>



<p>When this became slow and brittle, the industry swung the pendulum the other way: <strong>“Let’s just decentralize everything. Hello, microservices!”</strong></p>



<p>But we simply traded one form of coupling (centralized) for another (implicit and distributed). Pure choreography at scale also breaks down: it’s hard to reason about, hard to evolve, and nearly impossible to govern. </p>



<p>The challenges around end-to-end processes weren&#8217;t solved by magic—we just shifted complexity around. I talked about it at length in talks like “<a href="https://www.slideshare.net/slideshow/complex-event-flows-in-distributed-systems/105355143" target="_blank">Complex event flows in distributed systems</a>” and dedicated a whole chapter in my book <a href="http://li" target="_blank">Practical Process Automation</a>.</p>



<p>So how to solve this dilemma? </p>



<h2 class="wp-block-heading" id="h.64zu60xrmv60">The solution: a logically central orchestration layer that&#8217;s operationally distributed</h2>



<p>Here’s the mindset shift: <strong>you can run one logical orchestration layer while keeping development and operations decentralized.</strong></p>



<p>To make this more concrete, let’s use the example of a retail bank support process (I pick this because it nicely shows how you can later swap in agentic AI).</p>



<h3 class="wp-block-heading" id="h.hwj0zygc4iws">The business orchestration platform and its orchestration layer</h3>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image1" class="wp-image-162807" height="820" src="https://camunda.com/wp-content/uploads/2026/04/image1-4-1.png" width="1999" /></figure>
</div>


<p>The business orchestration layer holds the <strong>process logic</strong>. It coordinates <em>what</em> needs to happen for the end-to-end process, not necessarily <em>how</em> each step is carried out. For that, you loop in existing IT systems, AI agents, and humans.</p>



<p>It’s important to define the right granularity for end-to-end processes, just as you would with any other capabilities of an organization. In my book <em>Enterprise Process Orchestration</em>, I use a framework based on business capability maps with five layers:</p>



<ol class="wp-block-list">
<li>Business areas</li>



<li>Customer journeys</li>



<li>End-to-end processes</li>



<li>Business capabilities</li>



<li>Integration capabilities (often referred to as tools in the Agentic AI space)</li>
</ol>



<p>The following picture shows a sample map for the bank support process on layers 3 to 5 (the layers internal to an organization).</p>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image3" class="wp-image-162811" height="1085" src="https://camunda.com/wp-content/uploads/2026/04/image3-2-1.png" width="1999" /></figure>
</div>


<p>In this map, business capabilities might be implemented by any means: custom software, SaaS, manual steps, AI agents, or a mix of them. The end-to-end process is also “just” a special kind of business capability: one that focuses on long-running coordination across boundaries along the customer journey.</p>



<p>But any capability that requires long-running coordination should leverage <strong>process orchestration, </strong>to avoid accidental complexity when implementing this individually again and again.</p>



<p>The question becomes: how do you do this at scale across an organization without recentralizing everything?</p>



<h2 class="wp-block-heading" id="h.o8df2edg86l5">Team topologies: the real enabler of decentralization</h2>



<p>The trick is <strong>not</strong>&nbsp;to centralize modeling or ownership. We’re big fans of the <em>Team Topologies</em>&nbsp;book and you can map its ideas directly to an enterprise-wide orchestration approach:</p>



<ul class="wp-block-list">
<li>A central<strong> platform team</strong> provides the orchestration platform as a self-service capability</li>



<li>Federated <strong>stream-aligned teams</strong> build and own their workflows end-to-end</li>



<li>A central <strong>enablement team</strong> helps federated teams adopt good modeling and integration patterns.</li>
</ul>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image4" class="wp-image-162805" height="1045" src="https://camunda.com/wp-content/uploads/2026/04/image4-1.png" width="1999" /></figure>
</div>


<p>Each stream-aligned team owns its piece of the process just like it owns its own microservice:</p>



<ul class="wp-block-list">
<li><a href="https://camunda.com/bpmn/" target="_blank">BPMN</a> models are versioned like (or together with) code</li>



<li>Workflows are deployed in units that make sense, independent of other teams</li>



<li>Teams test and monitor their own orchestration logic</li>



<li>No central modeling department, no process priesthood</li>
</ul>



<p>Every business capability that requires dedicated engineering will be implemented by a stream-aligned team. Some capabilities may indeed be delivered by standard off-the-shelf software or handled manually (think emails or spreadsheets), but a core set of capabilities in most organizations requires custom processes. That’s especially true for end-to-end processes.</p>



<p>This setup preserves autonomy while finally giving the organization a clear, observable view of the overall flow.</p>



<h2 class="wp-block-heading" id="h.co5yoyifm72p">Microservice compatibility and domain-driven design</h2>



<p>This approach is completely compatible with microservices thinking, because a microservice is just one way of implementing a business capability. This fits nicely with domain-driven design (DDD), which emphasizes clear component boundaries and bounded contexts.</p>



<p>The business orchestration layer “just” means that every microservice <strong>can</strong> leverage BPMN and process orchestration, but it doesn’t mean every service must embed a workflow engine. Teams can decide where it makes sense to introduce BPMN within their service boundary.</p>



<p>The orchestration layer is a <strong>technical capability</strong>&nbsp;the team has at its disposal (like a relational database or a message broker), not a mandate.</p>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image5" class="wp-image-162816" height="1064" src="https://camunda.com/wp-content/uploads/2026/04/image5-1.png" width="1999" /></figure>
</div>


<p>And with the end-to-end process being a business capability in its own right, you can also implement it as its own microservice. This clarifies ownership for end-to-end processes, which is a huge achievement. For years I’ve discussed with organizations in many industries how the lack of clear ownership for end-to-end processes causes friction, delays, and finger-pointing.</p>



<h2 class="wp-block-heading" id="h.k35tms8sm5us">AI requires agentic orchestration, not less orchestration</h2>



<p>When you add agentic AI, many of those capabilities may be implemented (or at least supported) by AI agents. In Camunda, we blend deterministic and dynamic behavior in BPMN models. We call this <strong>agentic orchestration</strong>: the orchestrated mix of structured workflows and AI-driven autonomy across agents, people, and systems.</p>



<p>This lets you choose the best approach for each task:</p>



<ul class="wp-block-list">
<li>A structured, deterministic process</li>



<li>A human-driven decision</li>



<li>A supervised AI agent</li>



<li>A fully autonomous AI agent</li>
</ul>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image6" class="wp-image-162802" height="682" src="https://camunda.com/wp-content/uploads/2026/04/image6-1.png" width="1999" /><figcaption class="wp-element-caption"><em>Example process: Loan support, with deterministic aspects, but also an AI agent at play in its center</em></figcaption></figure>
</div>


<p>The important bit: you can evolve over time. You might start with AI providing recommendations while humans stay fully in the loop, then gradually move to more automation as trust grows.</p>



<p>And you don&#8217;t just orchestrate agents from the outside as black boxes in a process. For agents you build on the platform, Camunda can also orchestrate them from the inside &#8211; injecting enforceable steps between an agent&#8217;s decision and its action. If an agent decides to send an email or approve a payout, the process can force a policy check or a human approval before anything actually happens. That&#8217;s what makes it safe to give agents real operational authority. </p>



<p>The great thing is that you don&#8217;t need one old-school process for deterministic steps and a second AI process for everything else. Agentic orchestration allows you to do this in one model: straight-through processing where the rules are clear, agent reasoning where judgment is needed, with the ability to dial autonomy up or down per step.</p>



<p>In a future where many autonomous AI agents carry out your core business operations, AI doesn’t reduce the need for orchestration; it <strong>increases</strong> it. Those agents still need to be coordinated, monitored, and governed to respond appropriately to situations like these:</p>



<ul class="wp-block-list">
<li>When should they be triggered?</li>



<li>How do you handle failures and contradictions?</li>



<li>When does a human need to step in?</li>



<li>How do you swap one AI provider for another?</li>
</ul>



<p>All of that is process logic and belongs in your orchestration layer. And we&#8217;ve been doing orchestration for business processes for years. Agentic orchestration is simply the next wave: the same enterprise-grade orchestration, now extended to AI agents.</p>



<h2 class="wp-block-heading" id="h.9aw6wqwz4y23">Platform requirements: what an orchestration engine must provide</h2>



<p>To make this viable, the underlying orchestration platform that powers the orchestration layer in your future business orchestration platform must support an enterprise-wide approach. It has to be built for scale and provide a handful of critical capabilities.</p>



<p>First, <strong>end-to-end processes need a shared language</strong> that both business and engineering can understand. BPMN fits this role very well. It allows you to describe flows according to all important <a href="http://x" target="_blank">workflow patterns</a>: steps and branching, decision points, compensations, timeouts and SLAs, work distribution between humans, systems, and AI. And it does this explicitly, not hidden in code or scattered across events.</p>



<p>Second, it needs to <strong>operate at scale</strong>. That’s not only about throughput and latency, but also about <em>how</em> teams can consume the platform, like:</p>



<ul class="wp-block-list">
<li>Self-service provisioning of dedicated clusters for high-demand use cases</li>



<li>Tenants on shared hardware for teams that don’t need their own cluster</li>



<li>A “catch-all” environment for a long tail of simple processes</li>
</ul>



<p>Third, it needs a <strong>flexible integration approach</strong> with features like:</p>



<ul class="wp-block-list">
<li>Out-of-the-box connectivity for common systems</li>



<li>Open APIs and SDKs for deep technical integrations (supporting MCP in the future)</li>



<li>The ability for your platform team to build and publish company-specific connectors and accelerators</li>
</ul>



<p>Fourth, it should support the <strong>platform play</strong> in your organization by:</p>



<ul class="wp-block-list">
<li>Fitting into your internal developer platform</li>



<li>Integrating with CI/CD, observability, and security</li>



<li>Providing a solid foundation for both process orchestration and agentic orchestration, blending deterministic and dynamic workflows</li>
</ul>



<p>Fifth, it must provide a real <strong>operational control room</strong>. There should be full visibility into every running case, every agent decision, every exception, with the ability to intervene, reroute, and continuously optimize. Observability and optimization shouldn&#8217;t be bolt-ons; they need to be built into the orchestration platform from day one.</p>



<p>Already today, Camunda delivers the core orchestration layer of your future business orchestration platform. It’s not just theory; it’s proven in production at large scale (see for example the <a href="https://camunda.com/learn/whitepapers/create-a-central-process-automation-platform/" target="_blank">whitepaper “How to Create a Central Process Automation Platform”</a>).</p>



<h2 class="wp-block-heading" id="h.60qcjocgbxt">This isn’t SOA 2.0—it’s distributed orchestration</h2>



<p>A central business orchestration layer doesn’t mean going back to ESB times. The difference is fundamental:</p>



<ul class="wp-block-list">
<li><strong>ESB centralized integration</strong> → orchestration centralizes <em>process orchestration methodology</em>, while solution development, operations, and integration remain decentralized.</li>



<li><strong>ESB tried to hide complexity</strong> → orchestration makes complexity observable and manageable.</li>



<li><strong>ESB broke ownership</strong> → orchestration strengthens domain and process ownership.</li>



<li><strong>ESB enforced one roadmap</strong> → orchestration enables team-level autonomy.</li>
</ul>



<p>From my experience, once architects see orchestration as <strong>infrastructure</strong>, not as a big central brain, the anxiety goes away.</p>



<p>And it gives you something you never really had before: a clear, adaptable, and observable view of how your business actually runs. In the age of AI, that will be the difference between companies that move forward and those that get left behind.</p>



<h2 class="wp-block-heading" id="h.bu2hseak316z">Final thoughts and where to go next</h2>



<p>The business orchestration layer will be a key component in the enterprise architecture of the future. For many organizations, it can make the difference between chaos and actually extracting value from introducing AI into their core business processes.</p>



<p>Getting there is, of course, a journey. But every journey starts with the first step. After outlining such a bold vision, the next move is simple: add process orchestration to one of your real business processes. Pick something relevant—something that solves an actual pain—but keep it small enough to deliver quick wins. Use that first project as a stepping stone toward the orchestrated enterprise you want to become over the next few years.</p>



<p>If you’d like to dive deeper into this journey, I can recommend the book <em><a href="https://www.amazon.de/Enterprise-Process-Orchestration-Hands-Technology/dp/1394309678/" target="_blank">Enterprise Process Orchestration</a></em>.</p>
<p>The post <a href="https://camunda.com/blog/2026/04/case-for-a-central-business-orchestration-layer-without-recentralizing-your-architecture/">The Case for a Central Business Orchestration Layer—Without Recentralizing Your Architecture</a> appeared first on <a href="https://camunda.com">Camunda</a>.</p>
