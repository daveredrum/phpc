---


---

<h1 id="chapter-12">Chapter 12</h1>
<h2 id="partitional-global-address-space-programming-pgas">Partitional Global Address Space Programming (PGAS)</h2>
<h3 id="context-for-upc">Context for UPC</h3>
<ul>
<li><strong>UPC</strong>: Unified Parallel C</li>
<li>most parallel programs are written using either:
<ul>
<li>message passing with an SPMD model (<strong>MPI</strong>) =&gt; scales easily on clusters, big machines</li>
<li>shared memory with threads in OpenMP, pThread =&gt; requires shared memory hardware</li>
</ul>
</li>
<li>Partitioned Global Address Space (<strong>PGAS</strong>)
<ul>
<li><strong>global</strong> address space like programming with threads =&gt; <strong>programmability</strong></li>
<li><strong>SPMD parallelism</strong> like most MPI programs =&gt; <strong>performance</strong></li>
<li><strong>local/remote distinction</strong> =&gt; <strong>performance</strong></li>
</ul>
</li>
</ul>
<h3 id="upc-execution-model">UPC Execution Model</h3>
<ul>
<li>a number of threads working independently in a SPMD fashion
<ul>
<li>number of threads: a program variable <strong>THREADS</strong></li>
<li>UPC threads are most often implemented as a full OS processes</li>
</ul>
</li>
<li><strong>MYTHREAD</strong> specifies thread index <strong>[0, THREADS-1]</strong></li>
<li><strong>upc_barrier</strong> is a global synchronization =&gt; all wait before continuing</li>
<li>compilation modes:
<ul>
<li>static threads mode:
<ul>
<li><strong>THREADS</strong> is specified at compile time by the user</li>
<li>the program my use <strong>THREADS</strong> as a compile-time constant</li>
</ul>
</li>
<li>dynamic threads mode
<ul>
<li>compiled code may be run with varying numbers of threads</li>
</ul>
</li>
</ul>
</li>
</ul>
<h3 id="upc-global-synchronization">UPC Global Synchronization</h3>
<ul>
<li>two basic forms of barriers
<ul>
<li><strong>barrier</strong>
<ul>
<li><code>upc_barrier</code>: block until all other threads arrive</li>
</ul>
</li>
<li><strong>split-phase barrier</strong>
<ul>
<li><code>upc_notify</code>: this thread is ready for barrier</li>
<li><code>upc_wait</code> wait for others to be ready</li>
</ul>
</li>
</ul>
</li>
<li>lock
<ul>
<li>represented by an opaque type <code>upc_lock_t</code></li>
<li>must be allocated before use</li>
<li>to use a lock:
<ul>
<li><code>void upc_lock(upc_lock_t *lock)</code></li>
<li><code>void upc_unlock(upc_unlock_t *lock)</code></li>
</ul>
</li>
<li>free a lock
<ul>
<li><code>void upc_lock_free(upc_lock_t *ptr)</code></li>
</ul>
</li>
</ul>
</li>
</ul>

