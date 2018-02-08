---


---

<h1 id="chapter-4.1">Chapter 4.1</h1>
<h2 id="message-passing-and-basic-mpi">Message Passing and Basic MPI</h2>
<h3 id="distributed-memory-vs.-shared-memory">Distributed Memory vs. Shared Memory</h3>

<table>
<thead>
<tr>
<th></th>
<th>Shared Memory</th>
<th>Distributed Memory</th>
</tr>
</thead>
<tbody>
<tr>
<td>Advantages</td>
<td>1. simpler to program <br> 2. implicit communication</td>
<td>1. natural automatic locality control <br> 2. runs everywhere <br> 3. scalability and performance <br> 4. no race conditions possible</td>
</tr>
<tr>
<td>Disadvantages</td>
<td>1. difficult to control locality <br> 2. race condition <br> 3. false sharing</td>
<td>1. low-level, complex programming <br> 2. large memory consumption due to replication of data</td>
</tr>
</tbody>
</table><h3 id="message-passing-libraries">Message Passing Libraries</h3>
<ul>
<li>all communication and synchronization requires <strong>subroutine calls</strong></li>
</ul>
<blockquote>
<p>program runs on a single processor is just like any sequential uni-processor program</p>
</blockquote>
<ul>
<li>MPI contains subroutines for:
<ul>
<li>information/enquiry</li>
<li>communication
<ul>
<li><strong>pairwise</strong>: send &amp; receive</li>
<li><strong>collective</strong>: scatter &amp; gather, etc.</li>
</ul>
</li>
<li>synchronization
<ul>
<li><strong>barriers</strong></li>
</ul>
<blockquote>
<p>no locks because there are no shared variables to protect</p>
</blockquote>
</li>
</ul>
</li>
</ul>
<h3 id="novel-features-of-mpi">Novel Features of MPI</h3>
<ol>
<li><strong>communicators</strong> encapsulate communication context for library safety</li>
<li><strong>datatypes</strong> reduce copyig costs and permit heterogeneity</li>
<li>multiple communication <strong>modes</strong> allow precise buffer management</li>
<li>extensive support for <strong>collective operations</strong> for scalable global communication</li>
<li><strong>process topologies</strong> permit efficient process placement and user views of process layout</li>
<li><strong>profiling interface</strong> encourages portable tools</li>
</ol>
<h3 id="hello-world-in-mpi">Hello World in MPI</h3>
<p><img src="https://lh3.googleusercontent.com/KlpQHzYbb7Eeh37eW_CY_EH3tgbXiPzaixeKT4kqTnchQ7AWXWAENT3MW1LuZaVhWuasYAKFTCY" alt="enter image description here"></p>
<ul>
<li>all MPI programs begin with <code>MPI_Init(&amp;argc, &amp;argv)</code> and end with <code>MPI_Finalize()</code></li>
<li><code>MPI_COMM_WORLD</code> designates all processes in the current MPI program</li>
<li><code>MPI_Comm_size(MPI_COMM_WORLD, &amp;size)</code> reports the total number of process and saves to <code>size</code></li>
<li><code>MPI_Comm_rank(MPI_COMM_WORLD, &amp;myrank)</code> reports the rank identifying the calling process, <strong>0 &lt;= myrank&lt;= size - 1</strong></li>
</ul>
<h3 id="process-creation-and-execution">Process Creation and Execution</h3>
<ul>
<li>compile: <code>mpicc -o &lt;exec&gt; &lt;file&gt;.c</code></li>
<li>execute: <code>mpirun -np &lt;proc&gt; &lt;exec&gt;</code></li>
</ul>
<h3 id="structure-of-mpi-functions">Structure of MPI Functions</h3>
<ul>
<li>general: <code>result = MPI_Xxx(...);</code></li>
</ul>
<h3 id="data-transmission">Data Transmission</h3>
<ul>
<li>identify communication partner
<ul>
<li>processes can be collected into <strong>groups</strong></li>
<li>message sent in a <strong>context</strong>, and must be received in the same <strong>context</strong></li>
<li><strong>group</strong> + <strong>context</strong> =&gt; <strong>communicator</strong></li>
<li>identify a process by its <strong>rank</strong> in the <strong>group</strong> associated with a <strong>communicator</strong></li>
<li>default communicator: <strong>MPI_COMM_WORLD</strong></li>
</ul>
</li>
<li>describing the transmitted data
<ul>
<li>format: <strong>(address, count, datatype)</strong></li>
<li><strong>datatypes</strong>
<ul>
<li>basic predefined data types, e.g. <strong>MPI_INT</strong>, <strong>MPI_FLOAT</strong></li>
<li>a contiguous array: <strong>MPI_Type_contiguous</strong></li>
<li>a strided block: <strong>MPI_Type_vector</strong></li>
<li>an indexed array: <strong>MPI_Type_indexed</strong></li>
<li>an arbitrary structure: <strong>MPI_Type_struct</strong></li>
</ul>
</li>
</ul>
</li>
<li>MPI tags
<ul>
<li>messages are sent with a <strong>user-defined interger tag</strong>, to assist the receiving process in identifying the message</li>
<li>in the range <strong>[0, MPI_TAG_UB]</strong></li>
</ul>
</li>
<li>basic <strong>send &amp; receive</strong>
<ul>
<li><strong>send</strong>
<ul>
<li><code>MPI_Send(start, count, datatype, dest, tag, comm)</code></li>
</ul>
</li>
<li><strong>receive</strong>
<ul>
<li><code>MPI_Recv(start, count, datatype, source, tag, comm, status)</code></li>
<li><code>tag</code> could be <strong>MPI_ANY_TAG</strong></li>
<li><code>status</code> could be allocated by the user via <code>MPI_Get_count(&amp;status, datatype, &amp;recv_count);</code> determining the number of elements received</li>
</ul>
</li>
</ul>
<blockquote>
<p><strong>send</strong> has to be paired with a <em>matching</em> <strong>receive</strong></p>
</blockquote>
</li>
</ul>
<h3 id="collective-operations-in-mpi">Collective Operations in MPI</h3>
<ul>
<li><strong>MPI_BCAST</strong> distributes data from one process to all others in a communicator</li>
<li><strong>MPI_REDUCE</strong> combines data from all processes in a communicator and returns it to one process</li>
</ul>
<blockquote>
<p><strong>SEND &amp; RECEIVE</strong> can be replaced by <strong>BCAST &amp; REDUCE</strong> in many numerical algorithms</p>
</blockquote>

