---


---

<h1 id="chapter-7">Chapter 7</h1>
<h2 id="shared-memory-hardware">Shared Memory Hardware</h2>
<h3 id="nomenclature">Nomenclature</h3>
<p><img src="https://lh3.googleusercontent.com/aHKQZGoV_PYAN05gsi8hat3OgM_uwWhA9ibVXM0hCneflTYLkf0wBDsV1HZRuUpBZWoSXnxYxVU" alt="enter image description here"></p>
<ul>
<li>Uniform Memory Access (<strong>UMA</strong>)
<ul>
<li>only one global physical memory</li>
<li>each processor has the same performance characteristics</li>
<li>dominates the server market</li>
</ul>
</li>
<li>Non-Uniform Memory Access (<strong>NUMA</strong>)</li>
</ul>
<h3 id="cache-coherence">Cache Coherence</h3>
<ul>
<li>e.g.<br>
<img src="https://lh3.googleusercontent.com/Z8_xJv7rBsI9vd1a7lW1yXt7CR-6IoZ_HOyS_sYnOFptKu7vQYMXju349ode117TxJ0ha_oJptQ" alt="enter image description here"></li>
<li>two possibilities for cache
<ul>
<li>write-back cache
<ul>
<li>each update to a cache also updates the original memory location</li>
</ul>
</li>
<li>write-through cache
<ul>
<li>the original memory location is updated eventually, e.g. when the cache line is <strong>out</strong> from cache</li>
</ul>
</li>
</ul>
</li>
<li><strong>snooping</strong> on the bus<br>
<img src="https://lh3.googleusercontent.com/RAiGlDtfDPmrPlGcQ0J175VAihVW27Kx2aKt95TbYEGk6prfedTE9OmGcfPoCA2B375nHUYyCBY" alt="enter image description here">
<ul>
<li>cache controllers can snoop on the bus and see the transaction in the same order</li>
<li>cache controllers can take action if a bus transaction is <strong>relevant</strong></li>
<li>actions for relevant transactions: <strong>invalidate</strong>, <strong>update</strong>, <strong>supply value</strong></li>
<li>two types of protocols
<ul>
<li><strong>invalidation protocols</strong>: invalidate replicas if a processor writes a location</li>
<li><strong>update protocols</strong>: update replicas with the written value</li>
</ul>
</li>
</ul>
</li>
<li>directory based cache coherence
<ul>
<li>update information is kept in a directory data structure =&gt; <strong>bit map</strong></li>
</ul>
</li>
</ul>
<h3 id="memory-consistency-models">Memory Consistency Models</h3>
<ul>
<li>Sequential Consistency (<strong>SC</strong>)
<ul>
<li>a multiprocessor is <strong>sequentially consistent</strong> if the result of any execution is the same as if:
<ul>
<li>the operations of all the processors were executed in <strong>same sequential order</strong></li>
<li>the operations of each individual processor appear in this sequence in the order specified by its program</li>
</ul>
<blockquote>
<p>processors take turns to access the memory</p>
</blockquote>
</li>
<li>problems:
<ul>
<li>it limits reordering and other compiler/hardware transformations</li>
<li>leads to an overly complex implementation</li>
</ul>
</li>
</ul>
</li>
</ul>

