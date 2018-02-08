---


---

<h1 id="chapter-3-parallel-computing-concepts-terminology-platforms">Chapter 3: Parallel Computing: Concepts, Terminology, Platforms</h1>
<h3 id="task-decomposition">task decomposition</h3>
<ul>
<li>types
<ul>
<li><strong>static decomposition</strong>: tasks and dependencies are known before execution starts</li>
<li><strong>dynamic decomposition</strong>: new tasks are generated on-the-fly</li>
<li>granularity
<ul>
<li><strong>fine-grained</strong>: large number of small tasks</li>
<li><strong>coarse-grained</strong>: small number of large tasks</li>
</ul>
</li>
</ul>
</li>
<li>task dependency graph<br>
<img src="https://lh3.googleusercontent.com/3ReG6fve1sE0uNhvVoVjIxFNIBrW0d4kKdcM95Lp47eKyejBso4TXNoUnrQ6wDsOBIpLDmp7EfE" alt="enter image description here">
<ul>
<li>a task can only be executed when all dependencies are met</li>
<li>can form a directed acyclic graph (<strong>DAG</strong>)</li>
</ul>
</li>
<li>task interaction graph<br>
<img src="https://lh3.googleusercontent.com/6Xran04aocZ3G4tWMnnvWey3xLkY7oQSudqfO-x8jWz3OXO5YjuM1xmso_3VMMWDtdeUA8ZdzkY" alt="enter image description here">
<ul>
<li>formalizes interactions between tasks that are not dependencies</li>
</ul>
</li>
</ul>
<h3 id="decomposition-techniques">decomposition techniques</h3>
<ul>
<li>
<p>data decomposition =&gt; domain decomposition</p>
<ul>
<li>recursive decomposition
<ul>
<li>divide and conquer</li>
<li>e.g. quick sort</li>
</ul>
</li>
<li>functional decomposition
<ul>
<li>often: pipelining</li>
</ul>
</li>
<li>exploratory decomposition
<ul>
<li>decomposition of solution search spaces</li>
<li>parallel search stops as soon as solution is found</li>
<li>often: trees</li>
</ul>
</li>
<li>speculative decomposition
<ul>
<li>pre-compute several possible results</li>
</ul>
</li>
</ul>
</li>
<li>
<p>speedup and efficiency</p>
<ul>
<li>definition
<ul>
<li>Tn: execution time on n cores</li>
<li>speedup Sn = T1 / Tn</li>
<li>efficiency En = Sn / n</li>
</ul>
</li>
<li><strong>Amdahl’s Law</strong>
<ul>
<li>the achievable speedup is limited by the serial (non-parallelizable) portion of an application</li>
</ul>
</li>
</ul>
</li>
<li>
<p>weak and strong scaling</p>
<ul>
<li>definition
<ul>
<li><strong>strong scaling</strong>: keep the problem size constant, hope for a linear decrease in execution time with an increasing number of cores</li>
<li><strong>weak scaling</strong>: increase the problem size in accordance to number of cores, hope for a constant execution time</li>
</ul>
<blockquote>
<p>strong scaling is harder to achieve, because the sequential portion will limit the achievable speedup</p>
</blockquote>
</li>
</ul>
</li>
</ul>
<h3 id="platforms">platforms</h3>

<table>
<thead>
<tr>
<th align="left">Programming Model</th>
<th align="left">Machine Model</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">Threads</td>
<td align="left">Shared Memory <br> Multithreading <br> Distributed Shared Memory</td>
</tr>
<tr>
<td align="left">Message Passing <br> (Partitioned Global Address Space)</td>
<td align="left">Distributed Memory <br> Global Address Space <br> Volunteer Computing</td>
</tr>
<tr>
<td align="left">Data Parallel</td>
<td align="left">SIMD Systems <br> Vector Systems</td>
</tr>
<tr>
<td align="left">Hybrid Parallel</td>
<td align="left">Hybrid Machines</td>
</tr>
</tbody>
</table><ul>
<li>parallel programming model
<ul>
<li>thread
<ul>
<li><strong>private variables</strong></li>
<li><strong>shared variables</strong></li>
<li>challenge: <strong>data race</strong> occurs when multiple threads read and write at the same time =&gt; fixed by locks</li>
</ul>
</li>
<li>message passing
<ul>
<li>consists of a collection of <strong>named processes</strong>, usually fixed at program startup time</li>
<li>logically shared data is partitioned over local processes =&gt; <strong>no shared data</strong></li>
<li>processes communicate by <strong>explicit send and receive</strong> pairs</li>
<li>Message Passing Interface (<strong>MPI</strong>) is the most commonly used software</li>
</ul>
</li>
<li>partitioned global address space
<ul>
<li>consists of a collection of <strong>named processes</strong>, usually fixed at program startup time</li>
<li>shared data is partitioned over local processes</li>
<li>logically shared data might be physically distributed</li>
</ul>
</li>
<li>data parallel programming
<ul>
<li>single thread of control consisting of <strong>parallel operations</strong></li>
<li>parallel operation applied to all of a data structure, usually an <strong>array</strong></li>
</ul>
</li>
</ul>
</li>
<li>machine model
<ul>
<li>shared memory
<ul>
<li>all processors are connected to a large shared memory</li>
<li>typically called Symmetric Multiprocessor (<strong>SMP</strong>)</li>
</ul>
</li>
<li>multithreaded processor
<ul>
<li>memory and some other states are shared</li>
</ul>
</li>
<li>distributed shared memory (<strong>DSM</strong>)
<ul>
<li>memory is <strong>logically shared</strong>, but <strong>physically distributed</strong></li>
</ul>
</li>
<li>distributed memory
<ul>
<li>each processor has its own memory and cache but cannot directly access another processor’s memory</li>
<li>each node has a Network Interface (<strong>NI</strong>) for all communication and synchronization</li>
</ul>
</li>
<li>global address space
<ul>
<li><strong>NI</strong> can directly access memory without interrupting the CPU</li>
</ul>
</li>
<li>internet/volunteer computing
<ul>
<li>e.g. SETI@Home</li>
</ul>
</li>
<li><strong>SIMD</strong> system
<ul>
<li>a single <strong>control processor</strong> issues each instruction</li>
<li>a large number of <strong>small processors</strong> execute the same instruction</li>
</ul>
</li>
<li>vector machines
<ul>
<li>vector architectures are based on <strong>a single processor</strong></li>
<li>multiple functional units, all perform the same operation</li>
<li><strong>vector processors</strong>: vector instructions operate on a vector of elements</li>
</ul>
</li>
</ul>
</li>
</ul>

