---


---

<h2 id="chapter-1-introduction">Chapter 1: Introduction</h2>
<h3 id="moores-law">Moore’s Law</h3>
<p>The number of transistors on a chip doubles roughly in 18-24 months</p>
<h3 id="the-intel-tick-tock-model">The Intel Tick-tock Model</h3>
<p>The model architecture alternates between innovations of the micro-architectures (<strong>uArch</strong>) and process shrinks</p>
<ul>
<li><strong>Tick</strong>: new uArch, same process</li>
<li><strong>Tock</strong>:  same uArch, shrink process</li>
<li>changed to a three-step-model in 2016: <strong>process-architecture-optimize</strong></li>
</ul>
<h3 id="benchmark-linpack">Benchmark: Linpack</h3>
<p>To solve the dense system of linear equations using <strong>LU factorization</strong></p>
<ul>
<li>
<p>peak performance</p>
<ul>
<li>some architectures achieve 70-90% of peak performance on Linpack</li>
<li>much less in real world apps: &lt; 10%</li>
</ul>
</li>
<li>
<p>recorded parameters:</p>
<ul>
<li>size of the solved systems</li>
<li>peak performance</li>
<li>processor type</li>
<li>interconnect</li>
<li>OS version</li>
</ul>
</li>
</ul>
<h3 id="parallel-vs.-concurrent-vs.--distributed">Parallel vs. Concurrent vs.  Distributed</h3>
<h4 id="parallel-computing">Parallel computing</h4>
<ul>
<li>more tightly coupled</li>
<li>components are used at the same time to achieve a specific goal</li>
<li>offen all nodes are exact replicas of each other in close physical proximity</li>
</ul>
<h4 id="concurrent">Concurrent</h4>
<ul>
<li>things that happen in the same time</li>
</ul>
<h4 id="distributed-computing">Distributed computing</h4>
<ul>
<li>usually refer to more loosely coupled systems</li>
<li>independent systems providing a service</li>
<li>often geographically distributed</li>
</ul>
<h3 id="principles-of-parallel-computing">Principles of Parallel Computing</h3>
<ul>
<li>find enough parallelism</li>
<li>find the right granularity</li>
<li>preserve sequential semantics</li>
<li>coordinate and synchronize</li>
<li>locality and load balance</li>
<li>performance measurement and modeling</li>
</ul>
<h3 id="parallelism-in-every-machine">Parallelism in every machine</h3>
<ul>
<li>bit-level parallelism (e.g. floating point operations)</li>
<li>instruction-level parallelism (e.g. pipeline mechanism)</li>
<li>memory system parallelism (e.g. overlap of memory operations)</li>
<li>parallelizing compilers</li>
<li>OS parallelism</li>
</ul>

