---


---

<h1 id="chapter-13">Chapter 13</h1>
<h2 id="sources-of-parallelism-and-locality-in-simulation">Sources of Parallelism and Locality in Simulation</h2>
<h3 id="overview">Overview</h3>
<ul>
<li>parallelism and data locality are both critical to performance
<ul>
<li>moving data is the most expensive operation</li>
</ul>
</li>
<li>real-world simulation problems have parallelism and locality
<ul>
<li>many objects operate independently of others</li>
<li>objects often depend much more on nearby than distant objects</li>
<li>dependence on distant objects can often be simplified</li>
</ul>
</li>
<li>scientific models my introduce more parallelism</li>
<li>many problems exhibit parallelism at multiple levels</li>
</ul>
<h3 id="discrete-event-systems">Discrete Event Systems</h3>
<ul>
<li>system are represented as
<ul>
<li>finite set of variables</li>
<li>the set of all variables values at a given time is called the <strong>state</strong></li>
<li>each variable is updated by computing a <strong>transition function</strong> depending on the other variables and external input</li>
</ul>
</li>
<li>system may be:
<ul>
<li><strong>synchronous</strong>: at each discrete timestep evaluate all transition function =&gt; <strong>state machine</strong></li>
<li><strong>asynchronous</strong>: transition functions are evaluated only if the inputs change, based on an <strong>event</strong> from another part of the system =&gt; <strong>event driven simulation</strong></li>
</ul>
</li>
<li>e.g. Game of Life =&gt; <em>domain decomposition</em></li>
</ul>
<h3 id="particle-systems">Particle Systems</h3>
<ul>
<li>system has:
<ul>
<li>a finite number of particles</li>
<li>moving in space according to Newton’s laws</li>
<li>time is continuous</li>
</ul>
</li>
<li>e.g. star in space with laws of gravity =&gt; usually <em>domain decomposition</em></li>
</ul>
<h3 id="lumped-variables">Lumped Variables</h3>
<ul>
<li>depends on continuous parameters =&gt; <strong>Ordinary Differential Equations (ODEs)</strong></li>
<li>system of “lumped” (grouped together) variables</li>
<li>may arise solving <strong>Sparse Matrices</strong> problem
<ul>
<li>sparse matrix-vector multiplication</li>
<li>solving a sparse linear system</li>
<li>e.g. sparse matrix in presenting connection in circuit</li>
</ul>
</li>
</ul>
<h3 id="continuous-variables">Continuous Variables</h3>
<ul>
<li>depends on continuous parameters =&gt; <strong>Partial Differential Equations (PDEs)</strong></li>
<li>solving the heat equation: <strong>graph and stencil</strong>
<ul>
<li>e.g. graph and 5 point stencil<br>
<img src="https://lh3.googleusercontent.com/K6BlkkE4l1YrFB3f1UWXSrckfw3XkMsWWf0pyAcWEPIuPcV53qoBjvqf6d2Olj4Cl2Dv4RLpMLrL" alt="enter image description here"></li>
</ul>
</li>
</ul>

