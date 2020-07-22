<h1 id="susy-technical-requirement">SuSy: Technical requirement</h1>
<h3 id="abstract">Abstract</h3>
<p>This document represents technical details for SuSy and recommendations on how to implement concrete interfaces. <em>Core principles of interfaces</em> and <em>abstractions</em> must not be violated.</p>
<hr>
<h3 id="table-of-contents">Table Of Contents</h3>
<p>This document consists of several parts. We’ll only dive into vital parts of the system.</p>
<ol>
<li>Gravity Node participation.</li>
<li>SuSy Extractor’s uniqueness and specifics.</li>
<li>Future extension of the App.</li>
</ol>
<hr>
<h4 id="gravity-node-participation">1. Gravity Node Participation</h4>
<p>Strictly speaking, the SuSy application conforms to all of the requirements specified by Gravity Protocol. This includes the existence of specific Nebulas (at least 2) and 2 specific extractors for each.</p>
<p>Comparing to <em>ordinary Gravity Protocol Node</em> It worth mentioning that <em>SuSy app</em> differs from it <em><strong>only by having specific nebulas and extractors</strong></em>. SuSy conforms to ledger constraints and its dependency is <em><strong>vital</strong></em>.</p>
<p>Gravity Node exists and operates <em>under the hood</em> of SuSy.</p>
<h4 id="susy-extractor’s-uniqueness-and-specifics.">2. SuSy Extractor’s uniqueness and specifics.</h4>
<p>As regards Extractor’s behavior, SuSy aims to set specific duties for it, such as:</p>
<ol>
<li>Management of payment state on both chains(target and source).</li>
<li>Results confirmation/declining</li>
<li>Observation of payments queue (which payment to operate at exact timeframe).</li>
</ol>
<p>Extractor operates mainly on <em><strong>fetching</strong></em> and <em><strong>delivering</strong></em> current info about the payments on specific chains. The chain info getters should be maintained using <em><strong>different adapters</strong></em> for specific blockchain because API differs. Adapters inside the extractor combine <em><strong>multiple</strong></em> chains compatibility.</p>
<p>Here the conclusion is that SuSy <em><strong>has only one extractor</strong></em>. <em><strong>Multiple chains compatibility</strong></em> suggests <em><strong>multiple instances of the same extractor</strong></em>. Such goal is achieved by *<strong>switching adapters</strong> inside extractor <em><strong>at runtime</strong></em>. <em>(the example is in the spec)</em>.</p>

