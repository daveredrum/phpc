---


---

<h1 id="chapter-4">chapter 4</h1>
<h2 id="more-on-mpi">More on MPI</h2>
<h3 id="mpi-collective-operations">MPI Collective Operations</h3>
<ul>
<li>synchronization
<ul>
<li><code>int MPI_Barrier(MPI_Comm comm)</code></li>
<li><strong>each</strong> process in the group of <code>comm</code> calls <strong>MPI_Barrier</strong></li>
<li>the call blocks until <strong>all</strong> process in the group of <code>comm</code> have caled <strong>MPI_Barrier</strong></li>
</ul>
</li>
<li>data movement
<ul>
<li>one to many
<ul>
<li>Broadcast<br>
<img src="https://lh3.googleusercontent.com/xUg0aWEjcM8aD-b9_VUWa1XsK7Y2RKGJAYLMhdX6dv8tAyv4s_z97C2ABotrpWj2KL8jlKuiWME" alt="enter image description here">
<ul>
<li><code>int MPI_Bcast(void *buf, int count, MPI_Datatype datatype, int source, MPI_Comm comm)</code></li>
<li>called by both the <strong>sender</strong> (or the root) and the <strong>receiver</strong></li>
</ul>
</li>
<li>Scatter<br>
<img src="https://lh3.googleusercontent.com/-lCmL8N8GlzdSJlxdDNzl0Qjo9UekoMLfxsU7KFrJkX5ODtzR7bCVUjMd_ew5CTEjXKRGPi7vKg" alt="enter image description here">
<ul>
<li><code>int MPI_Scatter(void *sendbuf, int sendcount, MPI_Datatype senddatatype, void *recvbuf, int recvcount, MPI_Datatype recvdatatype, int source, MPI_Comm comm)</code></li>
</ul>
</li>
</ul>
</li>
<li>many to one
<ul>
<li>Reduction	<img src="https://lh3.googleusercontent.com/sV11rTAjKXTWbPL9Gm_c5wM7OQVVbgsScrb2w8fms0k6HbKtjLuTJR1wtlKpM1LX8IerEYkOXRw" alt="enter image description here">
<ul>
<li><code>int MPI_Reduce(void *sendbuf, void *recvbuf, int count, MPI_Datatype, MPI_Op op, int target, MPI_Comm comm)</code></li>
<li><strong>MPI_Op</strong> can be a logical or arithmetic operation, or a user-defined operation</li>
</ul>
</li>
<li>Gather	<img src="https://lh3.googleusercontent.com/O8mdWOs4J_IrEYDZcWLIHmFKzfdxJGmdg9ORSpUYmlP3cNsNtJ9rY1m1ez-D388W4gcPtGpiKR8" alt="enter image description here">
<ul>
<li>inverse of <strong>scatter</strong></li>
<li><code>int MPI_Gather(void *sendbuf, int sendcount, MPI_Datatype senddatatype, void *recvbuf, int recvcount, MPI_Datatype recvdatatype, int target, MPI_Comm comm)</code></li>
</ul>
</li>
</ul>
</li>
<li>many to many
<ul>
<li>Alltoall	<img src="https://lh3.googleusercontent.com/tpkO4YxSOqv84BLmY0y5t3SQjUdO5LyQXFqUBAqY22AHxLRapIcc1jI4ouLgSUZVMd5YQI00hK0" alt="enter image description here">
<ul>
<li><code>int MPI_Alltoall(void *sendbuf, int sendcount, MPI_Datatype senddatatype, void *recvbuf, int recvcount, MPI_Datatype recvdatatype, MPI_Comm comm)</code></li>
<li>equivalent to a <strong>matrix transpose operation</strong></li>
</ul>
</li>
<li>Allgether<br>
<img src="https://lh3.googleusercontent.com/sY7tjgukqQNVmJ-jM4pvr3nQo2QjWdShWzG2KYh0tdfJQ0GDiLYuAh2grVYxWI_8ELGKyvF98-Y" alt="enter image description here">
<ul>
<li><code>int MPI_Allgather(void *sendbuf, int sendcount, MPI_Datatype senddatatype, void *recvbuf, int recvcount, MPI_Datatype recvdatatype, MPI_Comm comm)</code></li>
<li>like <strong>MPI_Gather</strong>, but the result is available on all processors</li>
</ul>
</li>
<li>Allreduce<br>
<img src="https://lh3.googleusercontent.com/oPB9Z64lQRf9fciZXoJS0U7OkmnsSzrXhtWk8vkZNovJOSwnqS1p4t5LyxsGUGDc9KtBd7osmI8" alt="enter image description here">
<ul>
<li><code>int MPI_Allreduce(void *sendbuf, void *recvbuf, int count, MPI_Datatype datatype, MPI_Op op, MPI_Comm comm)</code></li>
<li><strong>MPI_Op</strong> can be a logical or arithmetic operation, or a user-defined operation</li>
<li>result is available in all processes</li>
</ul>
</li>
<li>Scan<br>
<img src="https://lh3.googleusercontent.com/tLeS3XgT49-9svLVvLYwFlXKp0kd0M85NLJvEdPs1K48uZHJ8ncDork-TzmA7O-Ih7rR0Au9KMI" alt="enter image description here">
<ul>
<li><code>int MPI_Scan(void *sendbuf, void *recvbuf, int count, MPI_Datatype datatype, MPI_Op op, MPI_Comm comm)</code></li>
<li><strong>MPI_Op</strong> can be a logical or arithmetic operation, or a user-defined operation</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
<li>non-blocking operations in MPI
<ul>
<li>immediately return <strong>request handles</strong>, which can be <strong>tested for completion</strong> and <strong>waited on</strong></li>
<li>multiple completions are available</li>
<li>e.g. <strong>MPI_Isend &amp; MPI_Irecv</strong></li>
</ul>
</li>
<li>communication modes
<ul>
<li><strong>synchronous mode (MPI_Ssend)</strong>: send does not complete until a matching receive has begun =&gt; <strong>deadlock</strong></li>
<li><strong>buffered mode (MPI_Bsend)</strong>: user allocates enough memory to avoid <strong>deadlock</strong></li>
<li><strong>ready mode (MPI_Rsend)</strong>: user guarantees that a matching receive has been posted</li>
</ul>
</li>
</ul>
<h3 id="mpi-process-topologies">MPI Process Topologies</h3>
<ul>
<li>topology
<ul>
<li>define an intuitive name space</li>
<li>allow an effective mapping of processes to a hardware topology</li>
</ul>
</li>
<li>MPI supports
<ul>
<li>multidimensional grids/meshes and tori</li>
<li>arbitrary graphs</li>
</ul>
</li>
<li>virtual topology will be an attribute of a communication domain</li>
<li>processes can access th topology and the coordinates via the communicator</li>
</ul>

