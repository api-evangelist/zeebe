---
title: "Fewer CVEs in Your Camunda 8 Containers with Hardened Base Images"
url: "https://camunda.com/blog/2026/03/camunda-8-hardened-base-images/"
date: "Tue, 31 Mar 2026 11:00:00 +0000"
author: "Eyal Marantenboim"
feed_url: "https://camunda.com/feed/"
---
<p>Many of our customers run Camunda in their own environments—across cloud, hybrid, and self-managed deployments—where our container images are deployed into production clusters, scanned by internal security tooling, and evaluated as part of compliance processes. The security characteristics of those images directly affect your risk posture, and your security is a priority for us.</p>



<p>With that responsibility in mind, we revisited an important question:&nbsp;<strong>Can we structurally reduce the inherited risk in our base images for everyone who runs Camunda—not only in our managed SaaS offering, but also in the images you deploy yourselves?</strong></p>



<p>Rather than focusing only on downstream scanning and remediation, we looked at the foundation itself to address risk at its source, reduce recurring vulnerability triage, and create a more predictable security baseline for both our teams and our customers.</p>



<p>In our internal comparisons, Camunda 8 images built on hardened Minimus base images showed 354 fewer known common vulnerabilities and exposures (CVEs) at the base layer than images built on our previous base images over the same period.</p>



<h2 class="wp-block-heading" id="h.9ktmbmhlzpxq">The challenge: inherited vulnerabilities in container images</h2>



<p>When you deploy Camunda in your own environment, the container images that underpin core components become part of your security and compliance posture. Those images are scanned by your internal tools, reviewed by platform security teams, and often included in audit and risk management workflows. The characteristics of the base image therefore directly influence the volume of findings your teams need to assess and manage.</p>



<p>Container images are built in layers, combining application code with a language runtime, operating system libraries, and supporting utilities. Each layer introduces dependencies, and each dependency can introduce potential vulnerabilities.</p>



<p>Because Camunda services rely on language runtimes and underlying OS libraries, traditional base images can carry a substantial dependency footprint, which in turn can generate a steady stream of inherited CVEs.</p>



<p>Even when images are fully up to date, new vulnerabilities are continuously disclosed against upstream components. These inherited CVEs appear in registry scans, CI pipelines, and cluster-level security tooling across your environment. Many originate from lower-level packages that are not directly used by your application workloads but still surface in dashboards, reports, and policy checks.</p>



<p>For teams running Camunda, this can translate into recurring operational effort: reviewing newly disclosed CVEs, determining whether they apply, documenting risk decisions, and validating updates or mitigations. Even when a vulnerability is not exploitable in context, it still needs to be evaluated and often explained during internal reviews or audits.</p>



<p>Our goal was to reduce that background workload for you by addressing inherited vulnerabilities at their source. By reducing the number of CVEs present in the base layer itself, we can help lower the volume of findings that surface in your scans and make it easier for your teams to focus on issues that genuinely require action.</p>



<h2 class="wp-block-heading" id="h.y1t2eynfe287">Our approach: moving to hardened base images from Minimus</h2>



<p>To reduce inherited risk at the foundation of our container stack, we transitioned several core base images to <a href="https://www.minimus.io" target="_blank">hardened images from Minimus</a>. Minimus provides small, security‑hardened container images&nbsp;that reduce the operating system and runtime dependencies included in the image, while remaining compatible with standard language runtimes.</p>



<p>As part of our collaboration, Minimus also operates against clear service-level objectives (SLOs) for vulnerability remediation: when upstream fixes become available for CVEs in their base images, they rebuild and publish updated images within agreed timeframes. That gives us a cleaner, more predictable base layer and shortens the time between a disclosed CVE, a fixed base image, and an updated Camunda 8 image. </p>



<p>For customers running Camunda Self-Managed, this base layer matters because it sits underneath multiple platform components (for example, the Zeebe engine and gateway). If the base layer carries a large dependency footprint, those inherited packages (and their CVEs) show up repeatedly across scans, registries, and cluster policies.</p>



<h3 class="wp-block-heading" id="h.z073ig1uk1ln">A concrete example: Zeebe’s container image</h3>



<p>Starting in Q2 2026, Camunda’s Zeebe container build&nbsp;supports a hardened base option via build arguments. By default, the image uses a hardened OpenJRE base from Minimus (pinned by digest), with a public Temurin JRE fallback available when explicitly selected.</p>



<p>The <a href="https://github.com/camunda/camunda/blob/main/Dockerfile" target="_blank">Dockerfile</a>&nbsp;documents&nbsp;this choice clearly, making the base layer explicit and reproducible. This gives us a practical way to shrink the OS and runtime footprint for JVM-based components without changing application behavior.</p>



<h3 class="wp-block-heading" id="h.unv183ftwywt">Why this matters for Self-Managed customers</h3>



<p>Camunda Self-Managed deployments are run in environments our customers control—from Kubernetes clusters to VM-based infrastructure—and are integrated into their internal security, compliance, and vulnerability management workflows. The container images that underpin core components such as Zeebe, Operate, Tasklist, Optimize, and Identity are scanned in registries, evaluated by platform security teams, and often reviewed as part of audit processes.</p>



<p>When inherited CVEs are present in the base layer, they surface across multiple deployed services at once. That can translate into recurring triage cycles, exception handling, policy discussions, and documentation work—even when the underlying vulnerability is not exploitable in the context of a given workload.</p>



<p>By reducing inherited vulnerabilities at the base-image layer, we reduce that background noise across the entire Self-Managed footprint. Customers see fewer alerts in their dashboards, fewer findings to justify during audits, and a clearer signal when a vulnerability genuinely requires attention. The result is a more predictable security baseline across all deployed Camunda components, without requiring changes to application configuration or operational processes.</p>



<h2 class="wp-block-heading" id="h.n4hyqqdh7ah0">Scope of the change</h2>



<p>We applied this transition to four widely used base images in our environment: Node, OpenJDK, OpenJRE, and PHP. These images underpin multiple services and represent a meaningful portion of our container footprint.</p>



<p>To measure impact, we tracked CVE counts across two parallel tracks: traditional third-party images and hardened images from Minimus. Running scans against both sets of images using Grype, we were able to see the difference in CVEs between the two.</p>



<p>We looked at two distinct measurements:</p>



<ol class="wp-block-list">
<li>How many CVEs were eliminated from our stack as a result of changing our base images?</li>



<li>How many new CVEs did we avoid (ie, CVEs that would have impacted us with the old base images, but never impacted the hardened images).</li>
</ol>



<h2 class="wp-block-heading" id="h.c5tilhe6afgq">Immediate results: 354 fewer vulnerabilities</h2>



<p>To answer the first question, we compared the CVEs found by Grype immediately before and after switching base images. Scanning the base images themselves showed us the following results—a total reduction of 354 CVEs. The Node, OpenJRE and PHP components below are all part of the Camunda application and our distributed images, while OpenJDK is used within our internal build process.</p>



<figure class="wp-block-table"><table><tbody><tr><td><strong>Base image</strong></td><td><strong>Date of Change</strong></td><td><strong>Original Image CVE Count</strong></td><td><strong>Hardened Image<br />CVE Count</strong></td><td><strong>CVE Reduction</strong></td></tr><tr><td>Node</td><td>January 2026</td><td>234</td><td>1</td><td>233</td></tr><tr><td>OpenJDK</td><td>November 2025</td><td>37</td><td>2</td><td>35</td></tr><tr><td>OpenJRE</td><td>November 2025</td><td>11</td><td>0</td><td>11</td></tr><tr><td>PHP</td><td>December 2025</td><td>75</td><td>0</td><td>75</td></tr><tr><td><strong>Total</strong></td><td></td><td><strong>357</strong></td><td><strong>3</strong></td><td><strong>354</strong></td></tr></tbody></table></figure>



<p>This was not the result of suppressing findings or changing scanner settings. The vulnerabilities simply weren’t present in the base layer.</p>



<h2 class="wp-block-heading" id="h.msllti9ljfdv">Ongoing reduction: eliminating the security noise</h2>



<p>Security posture is not static. New vulnerabilities are disclosed continuously as upstream projects evolve, and those disclosures can trigger alerts, reviews, patch work, rebuilds, and documentation.</p>



<p>After including the new base images in release versions of Camunda, we’ve monitored the ongoing impact of newly disclosed CVEs over time. A total of 147 new CVEs were disclosed against the traditional base images we used. Of these, only 3 impacted the new hardened images—a 97.9% reduction in new CVEs.</p>



<p>Here’s the per-image breakdown of those ongoing CVEs avoided:</p>



<figure class="wp-block-table"><table><tbody><tr><td><strong>Base Image</strong></td><td><strong>Camunda Component</strong></td><td><strong>Original Image</strong><br /><strong>New CVEs</strong></td><td><strong>Hardened Image<br />New CVEs</strong></td><td><strong>CVE Reduction</strong></td></tr><tr><td>Node</td><td>Console<br />Web-Modeler webapp</td><td>42</td><td>2</td><td>40</td></tr><tr><td>OpenJDK</td><td>Operate<br />Tasklist<br />Zeebe<br />Optimize<br />Connectors<br />Management Identity<br />Web-Modeler restapi</td><td>36</td><td>1</td><td>35</td></tr><tr><td>OpenJRE</td><td>Operate<br />Tasklist<br />Zeebe<br />Optimize<br />Connectors<br />Management Identity<br />Web-Modeler restapi</td><td>34</td><td>0</td><td>34</td></tr><tr><td>PHP</td><td>Web-Modeler websockets</td><td>35</td><td>0</td><td>35</td></tr><tr><td><strong>Total</strong></td><td></td><td><strong>147</strong></td><td><strong>3</strong></td><td><strong>144</strong></td></tr></tbody></table></figure>



<p>The practical impact here is less about a single snapshot and more about the recurring workload that <em>doesn&#8217;t</em>&nbsp;have to happen. When inherited CVEs continually appear, they create a recurring operational tax: triage cycles, exploitability assessments, policy discussions, risk documentation, rebuilds, retesting, and coordinated updates across services that share the same base.</p>



<p>By keeping the base layer clean, we reduce that recurring workload. Our teams can spend more time strengthening application-level security controls, improving reliability and performance, and delivering new platform capabilities, instead of repeatedly evaluating inherited OS- or runtime-level findings.</p>



<p>For our Camunda 8 Self-Managed customers, the benefit is similar: fewer inherited CVEs means fewer alerts, fewer documented exceptions, and less time spent proving that a finding is not exploitable in context. The end result is a more predictable baseline and a clearer signal when something genuinely needs attention.</p>



<p>This reflects an important shift: not just managing vulnerability volume, but reducing vulnerability surface area by design.</p>



<h2 class="wp-block-heading" id="h.ymeo8ublxzb3">What this means for you</h2>



<p>When you run Camunda, this base layer is integrated into your internal security, compliance, and vulnerability management workflows. By reducing inherited vulnerabilities at the source, we reduce the background noise and deliver key operational benefits to you:</p>



<ul class="wp-block-list">
<li><strong>Reduced operational tax:</strong>&nbsp;Fewer inherited CVEs means less time spent on recurring triage, documentation, and policy discussions.</li>



<li><strong>Cleaner scans:</strong>&nbsp;Fewer alerts in your dashboards and compliance reports.</li>



<li><strong>Faster time to value</strong>: Fewer blocking findings in early scans and reviews make it easier to move from evaluation to production, and to roll out updates without repeated rework.</li>



<li><strong>Clearer signal:</strong>&nbsp;Your teams can focus on vulnerabilities that genuinely require attention, not inherited OS-level findings.</li>
</ul>



<h2 class="wp-block-heading" id="h-continuing-to-strengthen-the-foundation">Continuing to strengthen the foundation</h2>



<p>This base image transition is one example of how we continue to invest in secure-by-design architecture across the Camunda platform. By adopting hardened images from Minimus and reducing inherited vulnerabilities at the source, we have strengthened our container security posture and reduced attack surface across multiple services.</p>



<p>Security is ongoing work. Foundational layers matter—especially when our customers depend on secure, reliable deployments in their own environments—and we will continue to evaluate and improve them as our platform evolves.</p>



<p></p>
<p>The post <a href="https://camunda.com/blog/2026/03/camunda-8-hardened-base-images/">Fewer CVEs in Your Camunda 8 Containers with Hardened Base Images</a> appeared first on <a href="https://camunda.com">Camunda</a>.</p>
