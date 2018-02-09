---


---

<h1 id="chapter-8">Chapter 8</h1>
<h2 id="programming-shared-memory-machines">Programming Shared Memory Machines</h2>
<h3 id="the-shared-memory-programming-model">The shared Memory Programming Model</h3>
<p><img src="https://lh3.googleusercontent.com/1uxJGMCePgD1A1pN0eQvq9moPL56katARp0u7riWesLBMZNtrQZNzTTmkxT078OMdp21-fZ8mXQ" alt="enter image description here"></p>
<ul>
<li>program is a collection of threads of control</li>
<li>each thread has a set of <strong>private variables</strong> and a set of <strong>shared variables</strong></li>
<li>threads <strong>communicate implicitly</strong> by writing and reading shared variables</li>
<li>threads coordinate by <strong>synchronizing</strong> on shared variables</li>
</ul>
<h3 id="common-notions-of-thread-creation">Common Notions of Thread Creation</h3>
<ul>
<li>cobegin/coend
<ul>
<li>statements in block may run in parallel</li>
<li>cobegins may be nested</li>
</ul>
</li>
<li>fork/join
<ul>
<li>forks procedure in job1 and runs in parallel in job2</li>
<li>wait at join point if it’s not finished</li>
</ul>
</li>
<li>future
<ul>
<li>expression evaluated in parallel</li>
</ul>
</li>
</ul>
<h3 id="posix-threads">POSIX Threads</h3>
<ul>
<li><strong>POSIX</strong>: Portable Operating System Interface for UNIX</li>
<li><strong>Pthreads</strong>
<ul>
<li>the POSIX threading interface</li>
<li>create POSIX threads via <code>int pthread_create(pthread_t *, const pthread_attr_t *, void * (*)(void *), void *);</code></li>
<li><strong>Barrier</strong>
<ul>
<li>especially common in <strong>SPMD</strong> (Single Program Multiple Data)</li>
<li><code>pthread_barrier_t b</code> create barrier</li>
<li><code>pthread_barrier_init(&amp;b,NULL,3)</code> initialize the barrier</li>
<li><code>pthread_barrier_wait(&amp;b)</code>	wait a barrier</li>
</ul>
</li>
<li><strong>Mutex</strong> (mutual exclusion, also: <strong>lock</strong>)
<ul>
<li><strong>acquire</strong> + <strong>release</strong></li>
</ul>
</li>
<li><strong>semaphore</strong>
<ul>
<li>allows k threads simultaneous access</li>
</ul>
</li>
</ul>
</li>
<li>pitfalls
<ul>
<li>data race bugs are very hard to find because they can be intermittent</li>
<li>deadlocks are usually easier, but can also be intermittent</li>
</ul>
</li>
</ul>
<h3 id="openmp">OpenMP</h3>
<ul>
<li><strong>Open</strong> specification for <strong>Multi-Processing</strong></li>
<li>execution model: <strong>fork-join</strong>
<ul>
<li><strong>sequential region</strong> =&gt; <strong>master thread</strong></li>
<li><strong>parallel region</strong> =&gt; <strong>team threads</strong></li>
<li>an <strong>implicit barrier</strong> at the end of a parallel region</li>
</ul>
</li>
<li>create threads
<ul>
<li><code>#pragma omp parallel</code></li>
</ul>
</li>
<li>worksharing
<ul>
<li><code>#pragma omp for</code></li>
</ul>
</li>
<li>shared and private variables
<ul>
<li><strong>shared variables</strong> are accessible by all threads</li>
<li><strong>private variables</strong> are only accessible by one thread =&gt; loop variables is automatically privatized</li>
</ul>
</li>
<li>parallel loop
<ul>
<li>loop scheduling <code>#pragma omp for schedule(type[, size])</code>
<ul>
<li><strong>static</strong>: chunks of iterations of the specified size are distributed among threads in a <strong>round-robin</strong> fashion</li>
<li><strong>dynamic</strong>: thread request chunks of specified size <strong>from the runtime</strong></li>
<li><strong>guided</strong>: chunk size is proportional to remaining work</li>
<li><strong>auto</strong>: decision is made by compiler and/or runtime system</li>
<li><strong>runtime</strong>: decision is made by runtime selection</li>
</ul>
</li>
</ul>
</li>
<li>parallel section <code>pragma omp section [clause]</code>
<ul>
<li>each section is executed <strong>once</strong> by a thread in the team</li>
<li>a thread may execute <strong>more than one section</strong></li>
</ul>
</li>
<li>single &amp; master <code>pragma omp master/single [clause]</code>
<ul>
<li><strong>any thread</strong> can be chosen for a single construct</li>
<li>only the <strong>master thread</strong> can execute the master construct</li>
</ul>
</li>
<li>task
<ul>
<li>independent units of work</li>
<li>allows parallelization of irregular problems</li>
</ul>
</li>
<li>reduction <code>pragma omp parallel reduction(operator: list)</code>
<ul>
<li>perform a reduction on the variables that appear in <code>list</code> by applying the specified <code>operator</code></li>
</ul>
</li>
<li>thread synchronization in OpenMP
<ul>
<li><strong>barriers</strong>
<ul>
<li><code>#pragma omp barrier</code></li>
<li>wait until all threads arrive, then continue</li>
</ul>
</li>
<li><strong>critical sections</strong>
<ul>
<li><code>#pragma omp critical [name]</code></li>
<li>only one thread allowed at a time =&gt; <strong>mutex</strong></li>
<li>realizes <strong>mutex</strong> semantics for the code block</li>
</ul>
</li>
<li><strong>atomic operations</strong>
<ul>
<li><code>#pragma omp atomic \ statement</code></li>
<li>operations on numeric data</li>
<li>equivalent to using a critical section in updating a value</li>
</ul>
</li>
<li><strong>locks</strong>
<ul>
<li><strong>simple locks</strong>: a thread cannot acquire the lock again before releasing it</li>
<li><strong>nestable locks</strong>: count on how many times the lock is acquired by the same threads</li>
</ul>
</li>
</ul>
</li>
</ul>

