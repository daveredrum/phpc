---


---

<h1 id="chapter-6">Chapter 6</h1>
<h2 id="performance-analysis-and-efficient-mpi-programming">Performance Analysis and Efficient MPI Programming</h2>
<h3 id="analyzing-mpi-programs">Analyzing MPI Programs</h3>
<ul>
<li>profiling with <strong>IPM</strong> (Integrated Performance Monitor)</li>
<li>trace visualization with <strong>Vampir</strong></li>
<li>automatic trace analysis with <strong>Scalasca</strong></li>
</ul>
<h3 id="optimization-scenarios-for-mpi-programs">Optimization Scenarios for MPI Programs</h3>
<ul>
<li>communication settings
<ul>
<li>two messaging protocols
<ul>
<li><strong>eager</strong>: message+envelope is stored on the receiver side in a pre-allocated buffer, later copied to user buffer =&gt; <strong>small messages</strong></li>
<li><strong>rendezvous</strong>: receiver indicates when buffer is available, data is stored directly into this buffer =&gt; <strong>large messages</strong></li>
</ul>
</li>
<li>eager protocol might provide a performance improvement</li>
</ul>
</li>
<li>optimizing the process mapping
<ul>
<li>the mapping of MPI processes to cores of a machine can have a big influence on performance</li>
<li>e.g. <strong>fill</strong> mapping 1<br>
<img src="https://lh3.googleusercontent.com/SvQSypT_ojPNXl6D4LEXibU2EkNxcUgBNyBUcafMEr3Y3cY3YSzY2JSUGL46eBoozzlmCgyuOTY" alt="enter image description here">
<blockquote>
<p>each node has 16 connections to other nodes</p>
</blockquote>
</li>
<li>e.g. <strong>fill</strong> mapping 2<br>
<img src="https://lh3.googleusercontent.com/6yUZ3HDenXrRy0VoNYkLy3_EQ3JGO7JD8a8G0dCk3BhziBzPsi6n0CjqSTNgboPwlKXuFLa1DlM" alt="enter image description here">
<blockquote>
<p>each node has 12 connections to other nodes</p>
</blockquote>
</li>
<li>e.g. <strong>round-robin</strong> mapping<br>
<img src="https://lh3.googleusercontent.com/J97ZgHMPl78Esbfw47oldYXhZwMiC5r4NLyGcLeSBEI8JJLxNaLVMw9fSsGCoMIrWftTfCV0jU8" alt="enter image description here">
<blockquote>
<p>each node has 32 connections to other nodes</p>
</blockquote>
</li>
</ul>
</li>
<li>implicit serialization
<ul>
<li>e.g.<br>
<img src="https://lh3.googleusercontent.com/pvwhZI9LL0S94oOlbvGgoon4t6Bhtn79HiVtclkeepRuOhqoIJbX-NL62HiT6ymr4MAQuUvXXSA" alt="enter image description here">
<blockquote>
<p>no deadlock, but serialization might occur</p>
</blockquote>
</li>
<li>avoiding th serialization
<ul>
<li>change the order of sends and receives</li>
<li>use non-blocking communication</li>
</ul>
</li>
</ul>
</li>
<li>resource contention
<ul>
<li>occurs when multiple pairs or groups of processes communicate</li>
<li>communication patterns can also stress the network</li>
</ul>
</li>
<li>reducing communication volume
<ul>
<li>choose domain decomposition strategies such that the communication volume is minimized</li>
</ul>
</li>
<li>aggregating messages
<ul>
<li>alpha-beta model</li>
<li>aggregating into larger messages is beneficial</li>
</ul>
</li>
<li>collective communication
<ul>
<li>e.g.<br>
<img src="https://lh3.googleusercontent.com/U7jaGGghbpGzymHqm3zXZzA4IA6gffyIUH-cfVCgUbO6eX60kHRqUbOPJOKywCsBM4eS0ic1QvM" alt="enter image description here"></li>
<li><strong>MPI_Reduce</strong></li>
<li>from linear complexity to logarithmic complexity</li>
</ul>
</li>
<li>overlapping communication and computation
<ul>
<li>using non-blocking communications to avoid deadlock and to implement asynchronous communication</li>
<li><strong>hybrid</strong> programming via threads</li>
</ul>
</li>
</ul>

