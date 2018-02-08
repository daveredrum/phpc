---


---

<h1 id="chapter-2">Chapter 2:</h1>
<h2 id="review-of-computer-architecture-concepts">Review of Computer Architecture Concepts</h2>
<h3 id="peak-performance">Peak performance</h3>
<p>The theoretical maximum that the hardware can deliver under idealized conditions</p>
<h3 id="the-performance-equation">The performance equation</h3>
<p><img src="https://lh3.googleusercontent.com/86hOMvK-_AwCmHuhCnT3jDNSFBGLFtg86npjNAC4vc0MiJN9Oq4tA90lzgQwmvROK0vVXVLcNf0" alt="enter image description here"></p>
<ul>
<li>instruction count: count for the total number of performed instructions</li>
<li><strong>CPI</strong>: cycles per instructions</li>
<li>cycle time: the time for a complete cycle</li>
</ul>
<h3 id="parallelism-in-single-core-processors">Parallelism in single-core processors</h3>
<ul>
<li>
<p>characters:</p>
<ol>
<li>partially hidden from the programmer</li>
<li>partially exposed through the Instruction Set Architecture (<strong>ISA</strong>)</li>
</ol>
</li>
<li>
<p>Instruction level parallelism (<strong>ILP</strong>)</p>
<ul>
<li>
<p>pipelining</p>
<ul>
<li><strong>throughput</strong> (or bandwidth): how many loads per hour</li>
<li><strong>latency</strong>: how long does it take for one particular load</li>
<li>potential speedup: number of pipeline stages</li>
<li>limits:
<ol>
<li><strong>overhead</strong> prevents arbitrary division of work</li>
<li><strong>hazards</strong> prevent next instruction from executing during its designated clock cycle: <strong>structural hazards</strong>, <strong>data hazards</strong>, <strong>control hazards</strong></li>
<li><strong>superscalarity</strong> increases occurrance of hazards</li>
</ol>
</li>
</ul>
<blockquote>
<p>pipelining improves <strong>throughput</strong> but not <strong>latency</strong></p>
</blockquote>
</li>
<li>
<p>superscalar execution</p>
<ul>
<li>CPI &lt; 1 (launch more than one instruction per cycle)</li>
</ul>
</li>
<li>
<p>Out Of Order execution (<strong>OOO</strong>)</p>
<ul>
<li>allow instructions behind stall to proceed</li>
<li>lead to out-of-order completion</li>
</ul>
</li>
<li>
<p>Very Long Instruction Word (<strong>VLIW</strong>): compiler specifies what can run in parallel</p>
</li>
</ul>
</li>
<li>
<p>data level parallelism (<strong>DLP</strong>)</p>
<ul>
<li>Single Instruction Multiple Data (<strong>SIMD</strong>)
<ul>
<li>same stem of operations on independent data items</li>
<li>SIMD vs. Vector
<ol>
<li>vectors are usually much longer</li>
<li>have gather-scatter support</li>
<li>high bandwidth to memory</li>
</ol>
</li>
</ul>
</li>
</ul>
</li>
<li>
<p>thread level parallelism (<strong>TLP</strong>)</p>
<ul>
<li>programmer specifies independent threads of control</li>
<li>Simultanenous Multi-Threading (<strong>SMT</strong>) to use under-utilized on-chip resources</li>
</ul>
</li>
</ul>
<h3 id="the-vector-programming-model">The vector programming model</h3>
<ul>
<li>requires programmer to identify parallelism</li>
<li>many HPC applications are natural consumers of vector processing</li>
</ul>
<h3 id="the-memory-system-and-caches">The memory system and caches</h3>
<ul>
<li>the memory hierarchy<br>
<img src="https://lh3.googleusercontent.com/8OYeYl7HlV_YG-bZi3FY8Po9G3va9BqNxc6SSLsqWV381BjiQvkl-xChwYAbqQlxxhOE6SZuvhc" alt="enter image description here"></li>
</ul>
<blockquote>
<p>the memory hierarchy tries to exploit locality to improve average access latency</p>
</blockquote>
<ul>
<li>a high degree of <strong>locality</strong>:
<ul>
<li><strong>spatial locality</strong>: accessing things nearby previous access</li>
<li><strong>temporal locality</strong>: reusing an item that was previously accessed</li>
</ul>
</li>
<li><strong>Cache</strong> is fast memory which keeps copy of data in main memory, hidden from software
<ul>
<li><strong>cache hit</strong> =&gt; in_cache memory access, fast &amp; cheap</li>
<li><strong>cache miss</strong> =&gt; non_cache memory access, slow &amp; expensive</li>
</ul>
</li>
</ul>
<h3 id="matrix-multiply">Matrix multiply</h3>
<ul>
<li>important metrics:
<ul>
<li>computational intensity
<ul>
<li><strong>q = f / m</strong>, where f = number of arithmetic operations, m = number of memory elements moved between fast and slow memory</li>
</ul>
</li>
<li>machine balance</li>
</ul>
</li>
<li>naive (<strong>non-blocked</strong>) matrix multiply has low computational intensity</li>
<li>blocking (<strong>tiling</strong>) allow us to get an arbitrary large computational intensity</li>
</ul>

