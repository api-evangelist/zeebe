---
title: "Introducing Camunda’s Enhanced SDK Portfolio"
url: "https://camunda.com/blog/2026/04/introducing-camunda-enhanced-sdk-portfolio/"
date: "Thu, 16 Apr 2026 17:42:42 +0000"
author: "Josh Wulf"
feed_url: "https://camunda.com/feed/"
---
<p>This post is for developers creating Camunda 8 applications and interested in using our new SDKs for TypeScript, Python, and C#.</p>



<p>With Camunda 8.9, we release a suite of next-generation SDKs that have been developed from the ground up for human-LLM collaboration. These SDKs extend support for Camunda applications to more programming languages and introduce powerful new features that increase application reliability at runtime.</p>



<p>We started development of these SDKs after observing LLMs struggling with edges in our existing SDK design.  With these enhanced SDKs, what were previously latent runtime errors in production are now inexpressible by construction in the IDE.</p>



<p>That&#8217;s the central promise of Camunda&#8217;s enhanced SDK portfolio, released with Camunda 8.9. Alongside a supported Python SDK and a Technical Preview of the C# SDK, this release delivers a fundamentally different approach to SDK correctness—one that has been years in the making.</p>



<p>The new SDKs join the long-lasting Java/Spring SDK and the Node.js SDKs, and the enhanced TypeScript SDK first released with 8.8. Together they fulfill the polyglot ecosystem vision unlocked by the Public API (Orchestration Cluster API) release in Camunda 8.8.</p>



<p>Full support for the C# SDK is coming in 8.10. The Technical Preview gives you a stable foundation to build on now, with a clear path to full support. We don&#8217;t anticipate major changes—and your feedback between now and 8.10 is what closes that gap.</p>



<h2 class="wp-block-heading" id="h.tywv12qdkr2k">The engineering approach</h2>



<p>The design draws on nearly a decade of continuous Camunda 8 SDK development, organized into four layers:</p>



<ul class="wp-block-list">
<li>Structural correctness</li>



<li>Developer ergonomics</li>



<li>Performance</li>



<li>Security</li>
</ul>



<p>The initial motivation for this work came from watching an LLM write a Camunda application using the 8.7 Node.js SDK. The LLM produced code that type-checked correctly, but failed at runtime. Looking at the code, the defect was visible, but undetectable by anything other than experienced engineer reasoning or a runtime error.</p>



<p>We asked the question: “<em>if a Camunda engineer can tell by looking at the code that it will fail at runtime, how do we make the compiler able to detect this?</em>”</p>



<h3 class="wp-block-heading" id="h.6ef85b8h7b3c">Structural correctness</h3>



<p>Each enhanced SDK is generated directly from the OpenAPI specification for the Camunda 8 Public API (Orchestration Cluster REST API), giving it complete API coverage with a 1:1 type surface matching the server release.</p>



<p>But coverage alone isn&#8217;t enough. Camunda&#8217;s API specification encodes an additional semantic layer—the Camunda domain type system. Entities like <code class="">ProcessDefinitionKey</code> and <code class="">ProcessDefinitionId</code> are serialized as primitive strings over the wire, but are type-disjoint in the Camunda engine domain. The enhanced SDKs carry this distinction into the compiler. An entire class of semantic substitution errors—ones that would previously only surface at runtime in production—becomes impossible to express in the IDE.</p>



<p>Here is an example of code that would previously pass type checking and compilation, but would fail at runtime (example written in C#):</p>



<pre class="wp-block-prismatic-blocks"><code class="language-csharp">var deploymentResponse = await camunda.DeployResourcesFromFilesAsync([“resources/model.bpmn”]);
var processDefinitionId = deploymentResponse.Processes[0].ProcessDefinitionKey;
var processInstance = await camunda.CreateProcessInstanceAsync(new ProcessInstanceCreationInstructionById(
    {
        ProcessDefinitionId = processDefinitionId
    }  );
</code></pre>



<p>The error is easy to make and easy to miss: in the second statement, the programmer has assigned the process definition <em>key</em> from the deployment response to a local variable, and then in the third statement used that variable as a process definition <em>id</em> when creating a process instance. <br /><br />In our earlier SDKs, this would typecheck, compile, and run—<em>but it would not work</em>. This class of defect results in a 4xx error at runtime when executed.</p>



<p>With LLMs enabling developers to produce thousands of lines of code, these errors require careful human review or exhaustive test coverage to catch. That method of quality assurance is late cycle detection, causing coordination friction and rework—when it works. You cannot guarantee complete coverage of all runtime states through these methods. These errors, if not detected in review or exercised in a test, enter production and can trigger on a conditional branch at any point in time.</p>



<p>We wanted to eliminate the possibility of this class of error. We accomplished this by encoding the business domain of the entity keys in an additional semantic layer in the OpenAPI specification, then reconstructing it in the type system of the enhanced SDKs.</p>



<p>In the image below, we see the behavior of the enhanced C# SDK in the IDE. All semantic substitution errors—such as mistakenly passing a <code class="">ProcessDefinitionKey</code> where a <code class="">ProcessDefinitionId</code> is required—are now a compile/design-time error, rather than a runtime error.</p>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image2" class="wp-image-162627" height="233" src="https://camunda.com/wp-content/uploads/2026/04/image2-3-1.png" width="1164" /></figure>
</div>


<p>Rather than relying on skill and luck—detecting these errors through manual code review or exercising the code path in an integration test—we made the error class inexpressible in the type system, allowing compilers to detect it and fail compilation/type-checking for human or LLM-generated code, and expression of this class of error in the IDE for human programmers. This moves defect detection from runtime to the point of authorship, collapsing the defect generation to detection loop for the entire class of defect. The result is enhanced runtime reliability and reduced cost of rework.</p>



<h3 class="wp-block-heading" id="h.eagoeabg76lv">Enhanced documentation</h3>



<p>Our focus on structural correctness extends to the SDK documentation. All code examples in the SDK documentation are type-checked during the build process. This means that any code examples that drift from the implementation cannot be published. This is the same collapse of the defect detection loop to the point of authorship, and quality gating is applied to documentation. In this release we’ve enhanced the generated API documentation with concrete examples, and also enriched our OpenAPI documentation with examples from each of the enhanced SDKs. Example: <a href="https://docs.camunda.io/docs/apis-tools/orchestration-cluster-api-rest/specifications/create-process-instance/" target="_blank">Create Process Instance</a>.</p>



<h2 class="wp-block-heading" id="h.2n96xwldxu2b">Developer ergonomics</h2>



<p>Around the generated core, we wrap an ergonomic layer built from experience designing and using developer-friendly Camunda SDKs. This layer handles application lifecycle concerns that live outside the OpenAPI specification: configuration hydration, smart connection defaults, convenience methods for loading deployment resources, job worker lifecycle management, and operation retry strategies.</p>



<p>The job worker framework in each SDK offers execution strategies appropriate to the language runtime—for example: threaded, sub-process, or asyncio in Python, event loop or multi-threaded in TypeScript—while keeping the developer experience idiomatic to each ecosystem.</p>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image1" class="wp-image-162630" height="412" src="https://camunda.com/wp-content/uploads/2026/04/image1-3-1.png" width="762" /></figure>
</div>


<h2 class="wp-block-heading" id="h.1wj9s57lthrs">Performance</h2>



<p>The most intractable category of defects in software implementation arises from runtime state management: time only appears at runtime. Race conditions and resource usage appear outside the type system and are impossible to reason about completely from compiler signals. &nbsp;</p>



<p>The answer to “how much throughput can I expect” remains “<em>it depends</em>”, but we now have detailed insight into optimal client architecture per language — for example, the best split between workers-per-process and processes, and the optimal number of workers for a given workload. Discovering the optimal architecture for a given use case and the resultant throughput requires investment.</p>



<p>The enhanced SDKs are validated against a performance matrix covering hundreds of scenarios across workload types. We run it in parallel across multiple lanes to keep total wall-clock time tractable (one run takes 392 hours, or ~50 hours parallelized), producing detailed data on throughput characteristics, bottlenecks, and regressions—and giving us the ability to both advise customers on the optimal architecture for their workload, and to add algorithms to the SDKs to manage distributed client adaptation.</p>



<p>The enhanced SDKs include client-side adaptive backpressure management using an AIMD algorithm inspired by TCP congestion control, tuned to Camunda&#8217;s distributed architecture. Enabled by default, it allows distributed client applications to sense the broker&#8217;s performance envelope through backpressure signalling and converge on optimal throughput automatically. This results in superior throughput performance for the same architecture with no user tuning.</p>



<p>Our testing reveals that the Orchestration Cluster REST API can deliver similar results to the gRPC for many use cases. It also means that we have a strong gate preventing performance regressing updates to an SDK.</p>



<p>As a representative example: our testing reveals that at the time of release, the enhanced TypeScript client plateaus when the client side is over-provisioned. When you hit the maximum throughput, if you add more worker containers, nothing happens to throughput (<em>to a degree—you can collapse anything with enough pressure</em>). With Python, on the other hand, throughput collapses faster as more workers are added. Python SDK users need to pay greater attention to their client architecture and matching the number of workers to the workload characteristics. A future feature release of the Python SDK will address this.</p>



<p>If you are not wedded to a particular language, performance testing shows that currently C# is the clear winner across the board. If you invest in performance testing and tuning your architecture then you can achieve greater throughput with Java and gRPC, but if you want something that is most likely to get the best performance with zero tuning, then you just deploy C# and use the REST API. </p>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image3" class="wp-image-162633" height="701" src="https://camunda.com/wp-content/uploads/2026/04/image3-1.png" width="1999" /></figure>
</div>


<p>Distributed systems have chaotic characteristics: a small change to any one of a large number of parameters can have exponential effects. Our engineers measure things like the impact of CPU L1 cache size on server performance. We are now engaged in the same level of analysis of the SDKs. Over subsequent releases, client architecture will dynamically adapt to real-time workload characteristics, optimizing performance automatically.</p>



<h2 class="wp-block-heading" id="h.m557nvuk698e">Security</h2>



<p>We are in a new world of security vulnerabilities. LLM assistance is accelerating the velocity of software development for hats of all colors. </p>



<p>Open Source development significantly accelerated development velocity over the past 20 years, but it has increased the vulnerable surface area for injection attacks. We continue to manage the tension between leveraging our participation in the open source community and securing the supply chain of our SDKs. </p>



<p>In order to reduce the vulnerable surface area for customers, in this release we have focused on “deleting the dependency graph” — reducing the number of dependencies that SDKs introduce into both customer and Camunda build chains. </p>



<p>For this release, we have significantly reduced the dependency graph. Representatively: we removed 124 direct and transitive dependencies from the TypeScript SDK across customer and Camunda systems between Camunda 8.8 and 8.9.</p>



<h2 class="wp-block-heading" id="h.dvsikqde7ef">Versioning</h2>



<p class="blog-note"><em>Bottom-line up-front: enhanced SDKs are major versioned, matched to the minor version of the server release.</em></p>



<p>SDK releases have always moved at a different cadence to the server.&nbsp;Previously, this forced a choice between two bad options: fully independent versioning (which required a compatibility decoder table) or locking major.minor to the server version (which collapsed all SDK changes into patch releases, obscuring real semver signal).<br /><br />The Java and Springboot clients, which were&nbsp;and in this release remain locked to the server version, require waiting for or forcing a server version release to ship fixes and features. </p>



<p>The enhanced SDKs take a third path: major version locked to server minor version. For the enhanced SDKs—TypeScript, Python, and the C# Technical Preview in this release—release 9.y.z of an enhanced SDK has a 1:1 type surface with Camunda 8.9. Release 10.y.z maps to Camunda 8.10. No decoder table.</p>



<p>The stronger compiler guarantees of runtime reliability provided by the new SDKs—enhanced compiler reasoning about the runtime behavior of customer applications when integrated with the Camunda server—mean that the lock between the SDK type system and the API surface introduces a more significant boundary for SDK / API version matching.</p>



<p>This means you can target a specific server runtime by changing the SDK dependency major version. The compiler will tell you if your application is safe to run: downgrading the major version surfaces unsupported operations; upgrading it reveals opportunities for stronger exhaustiveness checks.</p>



<p>An SDK major version increment signals the boundary of complete compiler reasoning about runtime reliability—not instability or breaking runtime changes. SDK features and fixes continue to follow accurate semantic versioning within that major. And when a runtime reaches end of life—Node.js v20 in April 2026, for example—we can remove it from the supported matrix cleanly, without constraining the SDK to a feature set that no longer has a future.<br /><br />We accurately signal feature and fix release in the semantic versioning of the enhanced SDKs by using the major version as the signal for the compiler reasoning boundary, matched to the server minor version, and using the feature and fix version for SDK features and fixes.</p>



<h2 class="wp-block-heading" id="h.3xlmyfq0j22o">Let’s go!</h2>



<p>The enhanced SDK portfolio is the foundation for what comes next. As Camunda&#8217;s Public API surface grows with each server release, the enhanced SDKs grow with it—automatically, correctly, with compiler-verified guarantees at every step. The goal has always been to let developers build on Camunda with confidence: confidence that their code is correct, that their integration is complete, and that the platform beneath them is one they can rely on for the long term.</p>



<p>If you are a Java developer and wondering, “<em>How do I get this goodness?</em>” it’s not in this release, but it is coming. The greenfield polyglot SDKs have been the proving ground for this new approach and feature set. Because they are greenfield releases, we are able to innovate faster. Managing the integration of existing customer codebases and versioning expectations requires a greater level of planning and management. We’re working on it now.</p>



<p>Read more about the technical characteristics of each of our enhanced SDKs in the <a href="https://docs.camunda.io/docs/apis-tools/working-with-apis-tools/" target="_blank">API Clients section of the Camunda Documentation</a>.<br /></p>
<p>The post <a href="https://camunda.com/blog/2026/04/introducing-camunda-enhanced-sdk-portfolio/">Introducing Camunda’s Enhanced SDK Portfolio</a> appeared first on <a href="https://camunda.com">Camunda</a>.</p>
