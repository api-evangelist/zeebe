---
title: "Meet c8ctl, the CLI that Makes Camunda 8 Feel Like Home"
url: "https://camunda.com/blog/2026/03/meet-c8ctl/"
date: "Thu, 26 Mar 2026 23:37:50 +0000"
author: "Volker Buzek"
feed_url: "https://camunda.com/feed/"
---
<p>Camunda introduces <code class="">c8ctl</code>&nbsp;(pronounced &#8220;cocktail&#8221;), a minimal-dependency command line interface (CLI) for Camunda 8.8+. <code class="">c8ctl</code> covers your entire development lifecycle, from inspecting your cluster topology through deploying and debugging processes. And with MCP proxy, your AI copilot talks directly to your cluster via MCP.</p>



<p>With this post, we have provided a bit of a tutorial with examples of how to use and work with c8ctl. Grab a drink. Let&#8217;s walk through it &nbsp;together, and you can learn more about how this CLI can work for you.</p>



<h2 class="wp-block-heading" id="h.aivjrh5x1kxr">Setting the scene</h2>



<p>You&#8217;ve got a Camunda 8.8+ cluster running. Maybe it&#8217;s local <a href="https://docs.camunda.io/docs/self-managed/quickstart/developer-quickstart/c8run/" target="_blank">via <code class="">c8run</code></a>, maybe it&#8217;s in our SaaS environment—either works. You&#8217;ve got BPMN files, DMN decisions, forms, and everything you need for your process. What you don&#8217;t have is the patience to click through a set of UIs just to determine if your cluster is alive or why your process might be stalled.</p>



<p>Enter `c8ctl`&nbsp;(alias `c8`). Built on the <a href="https://www.npmjs.com/package/@camunda8/orchestration-cluster-api" target="_blank"><code class="">@camunda8/orchestration-cluster-api</code></a>&nbsp;SDK, it keeps a single runtime dependency while exposing the full Camunda 8 REST API in your terminal. If you want to install the global binary, simply use <code class="">npm install @camunda8/cli -g</code>.</p>



<p class="blog-note"><em>Note: &nbsp;Be sure to </em><em><a href="https://docs.camunda.io/docs/next/apis-tools/c8ctl/getting-started/#prerequisites" target="_blank">configure all the prerequisites</a></em><em>&nbsp;so you can take advantage of this functionality. </em></p>



<p>With <code class="">c8ctl</code>, it’s like having a Camunda engineer built right into your terminal.</p>



<h2 class="wp-block-heading" id="h.geqqgd8nc0qo">Act 1: &#8220;Is anybody home?&#8221; or inspecting your cluster</h2>



<p>Every good development story starts with &#8220;does the thing even run?&#8221; Well, you can get that cluster status with a simple request to <code class="">c8ctl</code>:</p>



<pre class="wp-block-prismatic-blocks"><code class="">c8 get topology</code></pre>



<p>That&#8217;s your cluster handshake. You&#8217;ll see brokers, partitions, replication factors, and the cluster version. Think of it as the heartbeat check before you start operating.</p>



<p>Already have multiple environments? <code class="">c8ctl</code>&nbsp;has profile management baked in and can even auto-import profiles from <a href="https://docs.camunda.io/docs/components/modeler/desktop-modeler/" target="_blank">Camunda Desktop Modeler</a>.</p>



<p>Here are some examples of using <code class="">c8ctl</code>&nbsp;with profiles.</p>



<ul class="wp-block-list">
<li>To see what profiles you have available, use <code class="">c8 list profiles</code>. This will return something like this:<br /><figure class="wp-block-image aligncenter"><figure><img alt="Image11" src="https://camunda.com/wp-content/uploads/2026/03/image11-1.png" /></figure></figure></li>



<li>To see your active profile, use <code class="">c8 which profile</code>, which will return the profile name.</li>



<li>You can also switch to a new profile with <code class="">c8 use profile &lt;PROFILE_NAME&gt;</code>.</li>



<li>Get a look at a specific topology without changing context with <code class="">c8 get topology --profile=prod</code>.</li>
</ul>



<p>Need a quick look at what&#8217;s deployed? What process instances are running? Anything stalled or stuck? Take a look at some of these helpful commands to investigate process information.</p>



<ul class="wp-block-list">
<li>Want to see what process definitions are available? <code class="">c8 list process-definitions</code> or <code class="">c8 list pd</code> will return something like this:<br /><figure class="wp-block-image aligncenter"><figure><img alt="Image7" src="https://camunda.com/wp-content/uploads/2026/03/image7-2.png" /></figure></figure></li>



<li>What about active process instances? <code class="">c8 list process-instances</code> or <code class="">c8 list pi</code> will return something like this:<br /><figure class="wp-block-image aligncenter"><figure><img alt="Image1" src="https://camunda.com/wp-content/uploads/2026/03/image1-4.png" /></figure></figure></li>



<li>And you can even see if trouble is brewing by obtaining a list of incidents using <code class="">c8 list inc --state=ACTIVE</code>, which returns something like this if you have any active incidents:<br /><figure class="wp-block-image aligncenter"><figure><img alt="Image2" src="https://camunda.com/wp-content/uploads/2026/03/image2-2.png" /></figure></figure></li>
</ul>



<p>Then, of course, you can use the search command. This allows the use of wildcard&nbsp;matching, case-insensitive filters, and the ability to slice across process instances, user tasks, incidents, jobs, and variables.</p>



<ul class="wp-block-list">
<li>Find all the process definitions with <em>AI Loan</em>&nbsp;in the name with <code class="">c8 search pd --iname=&quot;ai loan*&quot;</code> which in this case returned the following:<br /><figure class="wp-block-image aligncenter"><figure><img alt="Image5" src="https://camunda.com/wp-content/uploads/2026/03/image5-3.png" /></figure></figure></li>



<li>Or to check for a specific error message (in this case error messages including <em>Exception</em>), use <code class="">c8 search inc --ierrorMessage=&#039;*Exception*&#039;</code>, which provides this for output in our example environment:<br /><figure class="wp-block-image aligncenter"><figure><img alt="Image13" src="https://camunda.com/wp-content/uploads/2026/03/image13-1.png" /></figure></figure></li>



<li>You can also find variables of a specific name with <code class="">c8 search variables --name=risk</code>, and the risk variable values are shown in the results: <figure class="wp-block-image aligncenter"><figure><img alt="Image4" src="https://camunda.com/wp-content/uploads/2026/03/image4-3.png" /></figure></figure></li>



<li>Or even all variables in a specific process instance by instance key, with <code class="">c8 search variables --processInstanceKey=2251799813685249 --fullValue</code>.</li>
</ul>



<p>The results of this inspection: </p>



<ul class="wp-block-list">
<li>Cluster inspected</li>



<li>Processes located</li>



<li>Incidents surfaced</li>
</ul>



<p>All from a single terminal. Let’s move on to the fun part.</p>



<h2 class="wp-block-heading" id="h.sb4m9sbaex89">Act 2: &#8220;Ship it&#8221; or deploying and managing processes</h2>



<p>You&#8217;ve modeled your BPMN, crafted your DMN, and polished all your forms. Now it’s time to deploy that process or maybe an entire project. Well, now you can do that directly from the command line with <code class="">c8ctl</code> .</p>



<p>It is as simple as one of the following commands. The first is to deploy the <code class="">order-process.bpmn</code> process with <code class="">c8 deploy &quot;./New Loan Request.bpmn&quot;</code>.</p>



<p>The results of a single BPMN deployment looks like the one shown below:</p>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image3" class="wp-image-162081" height="75" src="https://camunda.com/wp-content/uploads/2026/03/image3-3-1.png" width="542" /></figure>
</div>


<p>The second command will deploy an entire project: <code class="">c8 deploy &quot;Another Loan Application&quot;</code>.</p>



<p>Here, <em>Another Loan Application</em>&nbsp;is a directory. The results of an entire process application might look something like this:</p>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image15" class="wp-image-162093" height="147" src="https://camunda.com/wp-content/uploads/2026/03/image15-2-1.png" width="620" /></figure>
</div>


<p>Keep in mind, <code class="">c8ctl</code>&nbsp;isn&#8217;t just blindly pushing bytes. It understands your project structure. Do you have any building blocks (you might know about these, but check them out in <a href="https://docs.camunda.io/docs/next/apis-tools/c8ctl/development-workflows/#building-blocks-and-process-applications" target="_blank">our documentation</a>)? And what about the ability to not just deploy your process, but to run the instance too in a single command? Well, <code class="">c8ctl</code>&nbsp;will work for that as well. </p>



<p>Need to deploy <em>and</em>&nbsp;kick off an instance in one shot? The <code class="">run</code>&nbsp;command does exactly that:</p>



<pre class="wp-block-prismatic-blocks"><code class="">c8 run &#039;./Loan Process w AI.bpmn&#039; --variables&#039;{&quot;applicantID&quot;: 123456, &quot;requestedLoan&quot;: 125000, &quot;fullName&quot;: &quot;Joyce Jones&quot;, &quot;annualSalary&quot;: 455000, &quot;applicantEmail&quot;: &quot;joyce.johnson@camunda.com&quot;}&#039;</code></pre>



<p>In this case, the process is deployed and started and completed.</p>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image14" class="wp-image-162078" height="61" src="https://camunda.com/wp-content/uploads/2026/03/image14-2-1.png" width="316" /></figure>
</div>


<p>If we check this process in Camunda Operate, we will see the instance ID is started (and completed, in our case).</p>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image19" class="wp-image-162084" height="99" src="https://camunda.com/wp-content/uploads/2026/03/image19-1-1.png" width="1309" /></figure>
</div>

<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image16" class="wp-image-162088" height="820" src="https://camunda.com/wp-content/uploads/2026/03/image16-1-1.png" width="1463" /></figure>
</div>


<p>And managing the lifecycle is just as smooth. You can:</p>



<ul class="wp-block-list">
<li>Create a process instance using variables:<br /><code class="">c8 create pi --id=Process_loanR --variables&#039;{&quot;applicantID&quot;: 123456, &quot;requestedLoan&quot;: 125000, &quot;fullName&quot;: &quot;Joyce Jones&quot;, &quot;annualSalary&quot;: 455000, &quot;applicantEmail&quot;: &quot;&lt;a href=&quot;mailto:joyce.johnson@camunda.com&quot;&gt;joyce.johnson@camunda.com&lt;/a&gt;&quot;}&#039;</code><br /><br />This returns the process instance ID that is created.<br /><figure class="wp-block-image aligncenter"><figure><img alt="Image12" src="https://camunda.com/wp-content/uploads/2026/03/image12-1.png" /></figure></figure></li>



<li>Get details of the variables for the process instance with <code class="">c8 get pi 2251799814601077 --variables</code>. This returns JSON for all the variables for this process instance. An example of a subset of the response is shown below:<br /><figure class="wp-block-image aligncenter"><figure><img alt="Image9" src="https://camunda.com/wp-content/uploads/2026/03/image9-2.png" /></figure></figure></li>



<li>Cancel the process instance with <code class="">c8 cancel pi 2251799814610562</code>. This returns confirmation of the canceled process instance:<br /><figure class="wp-block-image aligncenter"><figure><img alt="Image10" src="https://camunda.com/wp-content/uploads/2026/03/image10-1.png" /></figure></figure></li>
</ul>



<p>In addition to the previous commands, you can also:</p>



<ul class="wp-block-list">
<li>Publish a message to a waiting catch event:<br /><code class="">c8 publish msg payment-received --correlationKey=order-42 --variables=&#039;{&quot;paid&quot;:true}&#039;</code></li>



<li>Complete a user task with variables:<br /><code class="">c8 complete ut 2251799813685250 --variables=&#039;{&quot;approved&quot;:true}&#039;</code></li>



<li>Resolve an incident (retry) after fixing the root cause:<br /><code class="">c8 resolve inc 2251799813685251</code></li>
</ul>



<h2 class="wp-block-heading" id="h.vlgp1e6wgtj9">Act 3: “The inner loop” or watch and wait mode</h2>



<p>But that’s only part of the story. You can use <code class="">c8ctl</code>&nbsp;to help you build and iterate faster.</p>



<h3 class="wp-block-heading" id="h.tvie5qcgzl4p">Watch mode: hot-reloading for process developers</h3>



<p>If you&#8217;ve ever worked with a frontend framework, you know the joy of saving a file and seeing changes instantly available. With <code class="">c8ctl</code>,&nbsp;you can bring that same energy to your process development. You can watch a directory using <code class="">c8 watch ./my-project</code> (where <em>my-project</em>&nbsp;is the folder name). Any modifications to that directory are monitored for changes.</p>



<p>That&#8217;s it. Every time you save a <code class="">.bpmn</code>, <code class="">.dmn</code>, or <code class="">.form</code>&nbsp;file, <code class="">c8ctl</code>&nbsp;redeploys it automatically. No manual deploy step, no tab-switching, no losing your flow. Edit in your modeler, save, and the new version is live on your cluster without further intervention.</p>



<h3 class="wp-block-heading" id="h.oq08h8adlqa9">Await: &#8220;Don&#8217;t call me, I&#8217;ll call you&#8221;</h3>



<p>After deployment, want to start an instance and wait for the result—all in one command? You can do this with <code class="">c8 await pi --id=order-process --variables=’{‘orderId’:”42”}</code>.</p>



<p>This creates a process instance and uses Camunda 8&#8217;s built-in server-side waiting to block until the process completes, returning the final variables. Perfect for testing short-lived processes or integration tests. Need a longer leash? Just add a <code class="">--requestTimeout=60000</code>&nbsp;(where <em>60000</em>&nbsp;is in milliseconds) to your command.</p>



<p>Want to go a step further? Try combining both <code class="">watch</code>&nbsp;and <code class="">await</code>&nbsp;and you get a ridiculously tight feedback loop for something like this:</p>



<ol class="wp-block-list">
<li>Edit your BPMN in the modeler.</li>



<li>Save (and watch as it auto-deploys).</li>



<li>Run <code class="">await</code>&nbsp;in another terminal (see the result).</li>
</ol>



<h2 class="wp-block-heading" id="h.9cn4huxqnk6j">Act 4: “Extend everything” or the plugin system</h2>



<p>When Camunda created <code class="">c8ctl</code>&nbsp;it was deliberately lean. But you may want or need more and the <a href="https://github.com/camunda/c8ctl/blob/main/PLUGIN-HELP.md" target="_blank">plugin system</a>&nbsp;lets you extend it without forking anything.</p>



<p>Plugins are regular <code class="">npm</code>&nbsp;packages with a <code class="">c8ctl-plugin.js</code>&nbsp;entry point. They get installed globally and appear right in <code class="">c8 help</code>.</p>



<ol class="wp-block-list">
<li>To provide a new plugin to c8ctl, simply enter <code class="">c8 init plugin my-awesome-tool</code>. <em>my-awesome-tool</em>&nbsp;is the name you want to assign to your plugin.</li>



<li>Then you can load your plugin from either npm or from a Git URL. From npm: <br /><code class="">c8 load plugin @camunda8/my-plugin-project</code><br /><br />From a Git URL:<br /><code class="">c8 load plugin --from https://github.com/camunda/my-plugin-project</code></li>



<li>Check that it is in your help now, by using <code class="">c8 help</code>.</li>
</ol>



<p>So you want to check out how to do this with a real-world example? <a href="https://github.com/camunda/c8ctl-plugin-diagram-renderer" target="_blank"><code class="">c8ctl-plugin-diagram-renderer</code></a> is a community-built plugin that renders a BPMN diagram right in the CLI—who says terminals can’t be visual?&nbsp;</p>



<p>Install the rendering plugin via <code class="">c8 load plugin --form https://github.com/camunda/c8ctl-plugin-diagram-renderer</code>.</p>



<p>Once installed, you can execute something like <code class="">c8 diagram &lt;PID&gt; --output ./diagramA.png</code> or even straight to the terminal (if yours support rendering graphics, such as iTerm2, Ghostty, or Kitty do) with <code class="">c8 diagram &lt;PID&gt;</code>.</p>



<p>This will create a PNG file of your diagram that will highlight where the process is at this time. The blue outline indicates complete/current steps. Here is an example output:</p>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image8" class="wp-image-162102" height="575" src="https://camunda.com/wp-content/uploads/2026/03/image8-1-1.png" width="1999" /></figure>
</div>


<p>And don’t forget, plugins get full access to the <code class="">c8ctl</code>&nbsp;runtime: SDK client factory, tenant resolution, output-aware logging, essentially, the whole toolbox. This code should help you get started with your plugin, it shows how to import <code class="">c8ctl</code>&#8216;s binary for use in the plugin:</p>



<pre class="wp-block-prismatic-blocks"><code class="">import type { c8ctlPluginRuntime } from &#039;@camunda8/cli/runtime&#039;;
const c8ctl = globalThis.c8ctl as c8ctlPluginRuntime;
const client = c8ctl.createClient();
const tenantId = c8ctl.resolveTenantId();
const logger = c8ctl.getLogger();
logger.info(`Operating on tenant: ${tenantId}`);</code></pre>



<p>Manage the full lifecycle: <code class="">load</code>, <code class="">upgrade</code>, <code class="">downgrade</code>, <code class="">unload</code>, <code class="">sync</code>, <code class="">list</code>. Plugins respect your profile, tenant, and output mode settings. And they are available in your help descriptions using <code class="">c8 help</code>&nbsp;when they provide metadata. It&#8217;s extensibility done right.</p>



<h2 class="wp-block-heading" id="h.am862p1eugal">Act 5: “Talk to your cluster via MCP” or the AI whisperer</h2>



<p>Now, this is where things get <em>really</em>&nbsp;interesting.</p>



<p><code class="">c8ctl</code>&nbsp;ships with an MCP (Model Context Protocol) proxy&nbsp;that bridges local AI tools—Claude Desktop, VS Code Copilot, or any MCP-compatible client to your Camunda 8 cluster:</p>



<pre class="wp-block-prismatic-blocks"><code class="">c8 mcp-proxy
c8 mcp-proxy –profile=&lt;PROFILE+NAME&gt;</code></pre>



<p><em>&lt;PROFILE_NAME&gt;</em>&nbsp;is the name of the Camunda profile to bridge.</p>



<p class="blog-note"><em>Note: You must have MCP enabled in your Camunda 8.9-alpha5 (or later) cluster.</em></p>



<p>What happens under the hood:</p>



<ul class="wp-block-list">
<li>Locally, <code class="">c8ctl</code>&nbsp;runs an MCP server over STDIO.</li>



<li>Remotely, it connects to Camunda&#8217;s <code class="">/mcp/cluster</code>&nbsp;endpoint (with Camunda 8.9+).</li>



<li>Authentication is handled automatically: token injection, 401 refresh, the works.</li>
</ul>



<p>The result? Your AI coding assistant can directly query your Camunda cluster for doing actions like:</p>



<ul class="wp-block-list">
<li>Listing process instances</li>



<li>Inspecting incidents</li>



<li>Searching for stuck jobs </li>
</ul>



<p>All through natural language, because the MCP bridge translates LLM tool calls into Camunda API requests.</p>



<p>This isn&#8217;t science fiction. Configure <code class="">c8 mcp-proxy</code> as a tool in your IDE&#8217;s AI setup, and your copilot literally becomes a Camunda operator.</p>



<h2 class="wp-block-heading" id="h.s10ipactbse4">Bonus act: Built for agents, not just humans</h2>



<p>Here&#8217;s a detail that sets <code class="">c8ctl</code>&nbsp;apart: it was designed from the ground up to be consumed by AI agents, not just human developers. That means you get the type of responses back from <code class="">c8ctl</code>&nbsp;that a developer would want to see.</p>



<h3 class="wp-block-heading" id="h.vgzoojtx8r43">JSON output mode</h3>



<p>Switch to JSON mode once, and every subsequent command emits machine-parseable output. Information and errors go to <code class="">stderr</code>, data goes to <code class="">stdout</code>.</p>



<p>So, assuming you are using text output and do a list of the process instances, you will see something like this:</p>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image6" class="wp-image-162095" height="101" src="https://camunda.com/wp-content/uploads/2026/03/image6-2-1.png" width="633" /></figure>
</div>


<p>Alternatively, if you switch to JSON output mode using <code class="">c8 output json</code> you will then see something like this:</p>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image18" class="wp-image-162099" height="593" src="https://camunda.com/wp-content/uploads/2026/03/image18-2-1.png" width="300" /></figure>
</div>


<h3 class="wp-block-heading" id="h.eq8eaper46ry">Context window diet with &#8211;fields</h3>



<p>LLMs operate within fixed token budgets. <code class="">c8ctl</code>&nbsp;respects those constraints by emitting only the required information and treating the context window as a scarce resource. That means you can limit your requests to only the information that you need, nothing more.</p>



<p>For example: <code class="">c8 list pi --fields Key,State,processDefinitionID</code>. Less noise, more signals.</p>



<h3 class="wp-block-heading" id="h.1d8od271ro25">Look before you leap with &#8211;dry-run</h3>



<p>For AI agents making mutating calls, <code class="">--dry-run</code>&nbsp;outputs the <em>exact</em>&nbsp;API request that <em>would</em>&nbsp;be executed—without actually doing it. Use <code class="">c8 create pi --id=order-process --dry-run</code>, and you will see something like this:</p>


<div class="wp-block-image">
<figure class="aligncenter"><img alt="Image17" class="wp-image-162087" height="142" src="https://camunda.com/wp-content/uploads/2026/03/image17-2-1.png" width="639" /></figure>
</div>


<p>The recommended AI agent workflow would be: dry-run → show user → confirm → execute. Safety by default.</p>



<h3 class="wp-block-heading" id="h.qh8a3pa79g2p">Machine-readable help</h3>



<p>In JSON mode, <code class="">c8 help</code>&nbsp;emits a fully structured command tree with all flags, types, aliases, and descriptions. An AI agent can bootstrap its understanding of the entire CLI in a single call.</p>



<h2 class="wp-block-heading" id="h.6mma2iv61w7c">The full SDLC, one CLI</h2>



<p>Let&#8217;s zoom out and trace a typical Camunda development lifecycle through <code class="">c8ctl</code>:</p>



<figure class="wp-block-table"><table><thead><tr><td><strong>Phase</strong></td><td><strong>What You Do</strong></td><td><strong>c8ctl Commands</strong></td></tr></thead><tbody><tr><td><strong>Setup</strong></td><td>Connect to your cluster</td><td><code class="">c8 add profile</code><br /><code class="">c8 use profile</code></td></tr><tr><td><strong>Verify</strong></td><td>Check the cluster is alive</td><td><code class="">c8 get topology</code><br /><code class="">c8 list pi</code></td></tr><tr><td><strong>Develop</strong></td><td>Edit BPMN/DMN/forms</td><td><code class="">c8 watch</code>&nbsp;(auto-deploys on save)</td></tr><tr><td><strong>Deploy</strong></td><td>Push to cluster</td><td><code class="">c8 deploy</code><br /><code class="">c8 run</code></td></tr><tr><td><strong>Test</strong></td><td>Run and verify</td><td><code class="">c8 await pi&lt;br&gt;c8 search pi&lt;br&gt;c8 get pi --variables</code></td></tr><tr><td><strong>Debug</strong></td><td>Find what&#8217;s broken</td><td><code class="">c8 search inc&lt;br&gt;c8 list jobs&lt;br&gt;c8 search variables</code></td></tr><tr><td><strong>Operate</strong></td><td>Fix and resolve</td><td><code class="">c8 get pd --xml&lt;br&gt;c8 resolve inc&lt;br&gt;c8 complete ut&lt;br&gt;c8 publish msg</code></td></tr><tr><td><strong>Extend</strong></td><td>Add custom capabilities</td><td><code class="">c8 load plugin&lt;br&gt;c8 init plugin</code></td></tr><tr><td><strong>Automate</strong></td><td>Let AI agents take the wheel</td><td><code class="">c8 mcp-proxy, --dry-run, --fields</code> <br />JSON mode</td></tr></tbody></table></figure>



<p>From first connection to AI-assisted operations. One CLI. One dependency. All the things.</p>



<h2 class="wp-block-heading" id="h.femczgx8ws0n">Getting started with a test drive</h2>



<p>If you want to try a few more things yourself, simply execute these commands to get started. Of course, you will need a BPMN process before you get started.</p>



<ul class="wp-block-list">
<li>Install <code class="">c8ctl</code>:<br /><code class="">npm install @camunda8/cli -g</code></li>



<li>See what’s out there by inspecting your cluster: <br /><code class="">c8 get topology</code></li>



<li>Deploy your first process:<br /><code class="">c8 deploy ./my-process.bpmn</code></li>



<li>Start watching:<br /><code class="">c8 watch</code></li>



<li>Await a process instance in another terminal window:<br /><code class="">c8 await pi –id=my-process</code></li>
</ul>



<p>Built with a single dependency and open source, <code class="">c8ctl</code>&nbsp;is a cocktail of good CLI design, Camunda expertise, and agentic engineering.</p>



<p class="blog-note"><em>Note: &nbsp;<code class="">c8ctl</code>&nbsp;is available on npm as <a href="https://www.npmjs.com/package/@camunda8/cli" target="_blank">@camunda8/cli</a>. Source on <a href="https://github.com/camunda/c8ctl" target="_blank">GitHub</a>.</em></p>



<p>Give it a spin. Your terminal will thank you.</p>
<p>The post <a href="https://camunda.com/blog/2026/03/meet-c8ctl/">Meet c8ctl, the CLI that Makes Camunda 8 Feel Like Home</a> appeared first on <a href="https://camunda.com">Camunda</a>.</p>
