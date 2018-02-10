---


---

<h1 id="chapter-9">Chapter 9</h1>
<h2 id="efficient-openmp-programming">Efficient OpenMP Programming</h2>
<h3 id="performance-analysis">Performance analysis</h3>
<ul>
<li>Instrumentation
<ul>
<li>adding measurement probes to the code to observe its execution</li>
</ul>
</li>
<li>measurement
<ul>
<li>profiling
<ul>
<li>summary statistics of performance metrics</li>
<li>reflects performance behavior of program entities</li>
<li>good for low-cost performance assessment</li>
<li>helps to expose performance bottlenecks and hotspots</li>
<li>via <strong>sampling</strong> and <strong>direct measurement</strong></li>
</ul>
</li>
<li>tracing
<ul>
<li>when and where events took place along a global timeline</li>
<li>save information in event record</li>
<li>used to reconstruct dynamic program behavior</li>
</ul>
</li>
</ul>
</li>
</ul>
<h3 id="profiling-openmp-with-ompp">Profiling OpenMP with ompP</h3>
<ul>
<li>ompP
<ul>
<li>profiling tool for OpenMP</li>
<li>based on <strong>preprocessor source code instrumentation</strong> and <strong>direct measurement</strong></li>
<li>independent of compiler and runtime</li>
<li>profiling report
<ul>
<li>header</li>
<li>region overview</li>
<li>flat region profile</li>
<li>callgraph and callgraph profiles</li>
<li>overhead analysis report</li>
<li>performance property detection report</li>
</ul>
</li>
</ul>
</li>
</ul>
<h3 id="optimization-techniques">Optimization Techniques</h3>
<ul>
<li>avoiding thread management overhead
<ul>
<li>an overhead associated with creaing threads =&gt; <strong>serial execution might be faster</strong> if there is very little work in a parallel region</li>
<li>OpenMP <strong>if clause</strong> can specify the standard serial version if condition is not met</li>
</ul>
</li>
<li>avoiding implicit barriers
<ul>
<li>there is an implicit barrier at the end of worksharing regions</li>
<li>remove this implicit barrier via <strong>nowait clause</strong></li>
<li>unsafe in some particular circumstances</li>
</ul>
</li>
<li>minimizing the number of parallel regions
<ul>
<li>avoid overhead of thread creation/destruction</li>
</ul>
</li>
<li>collapsing loops
<ul>
<li>via <code>#pragma omp for collapse(n)</code></li>
</ul>
</li>
<li>choosing the right loop scheduling clause
<ul>
<li><strong>avoid dynamic/guided scheduling</strong> unless necessary for load balancing</li>
</ul>
</li>
<li>avoiding false sharing
<ul>
<li>recall: <strong>separate threads work on adjacent data items that happen to reside on the same cache line</strong></li>
<li>local copies</li>
<li>array padding</li>
</ul>
</li>
</ul>

