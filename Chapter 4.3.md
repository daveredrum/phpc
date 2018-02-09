---


---

<h1 id="chapter-4.3">chapter 4.3</h1>
<h2 id="one-sided-communication-in-mpi">One-sided Communication in MPI</h2>
<p>Also known as Remote Memory Access (<strong>RMA</strong>)</p>
<h3 id="message-passing-vs.-remote-memory-access">Message Passing vs. Remote Memory Access</h3>
<ul>
<li>message passing
<ul>
<li><strong>"two-sided"</strong> semantics, coorperative model, where a procedure call on all involved processes is required</li>
<li>operations:
<ul>
<li><strong>send data</strong> to a process</li>
<li><strong>receive data</strong> from a process</li>
<li>performs a <strong>collective operation</strong> on data within a group of processes</li>
</ul>
</li>
<li>e.g. <strong>MPI_Send</strong>, <strong>MPI_Receive</strong></li>
</ul>
</li>
<li>Remote Memory Access (<strong>RMA</strong>)
<ul>
<li><strong>"one-sided"</strong> semantics, only the initiator of a transfer needs to make a procedure call</li>
<li>operations:
<ul>
<li><strong>put data</strong> to a remote process</li>
<li><strong>get data</strong> from a remote process</li>
<li><strong>updata data</strong> at a remote process</li>
<li>e.g. <strong>MPI_Put</strong>, <strong>MPI_Get</strong></li>
</ul>
</li>
</ul>
</li>
</ul>
<h3 id="advantages-of-one-sided">Advantages of One-sided</h3>
<ul>
<li>separation of data transfer and synchronization =&gt; <strong>can issue many operations and synchronize just once</strong></li>
<li>potentially better performance
<ul>
<li>less overhead, more optimization opportunities</li>
<li>good match for the <strong>RDMA</strong> (Remote Direct Memory Access) capabilities of modern interconnects</li>
</ul>
</li>
<li>a more natural model for some application areas
<ul>
<li>irregular applications</li>
<li>dynamically changing communication patterns</li>
</ul>
</li>
</ul>
<h3 id="mpi-rma-concepts">MPI RMA Concepts</h3>
<ul>
<li>
<p>MPI RMA Window Objects</p>
<ul>
<li>a <strong>window</strong> is local memory made accessible by RMA operations to a group of other processes
<ul>
<li>contiguous block</li>
<li>processes are specified by group associated with communicator</li>
</ul>
</li>
<li><strong>window object</strong> is the union of all windows in a group</li>
</ul>
<blockquote>
<ol>
<li>window can be empty</li>
<li>different displacement units are allowed, but not recommended</li>
</ol>
</blockquote>
</li>
<li>
<p>window creation</p>
<ul>
<li><strong>MPI_Win_create</strong>
<ul>
<li><code>int MPI_Win_create(void *base, MPI_Aint size, int disp_unit, MPI_Info info, MPI_Comm comm, MPI_Win *win);</code></li>
<li>user-allocated memory is exposed as window</li>
<li><strong>collective call</strong> on all processes in comm</li>
<li>returns a <strong>window object</strong> representing the window on all processes</li>
</ul>
</li>
<li><strong>MPI_Win_free</strong>
<ul>
<li>reclaims resources for window object</li>
<li>frees memory for MPI allocated windows</li>
</ul>
</li>
</ul>
</li>
</ul>
<h3 id="rma-communication-operations">RMA Communication Operations</h3>
<ul>
<li>basic operations
<ul>
<li><strong>MPI_Put</strong>: <code>int MPI_Put(const void *origin_addr, int origin_count, MPI_Datatype origin_dtype, int target_rank, MPI_Aint target_disp, int target_count, MPI_Datatype target_dtype, MPI_Win win);</code></li>
<li><strong>MPI_Get</strong>: <code>int MPI_Get(void *origin_addr, int origin_count, MPI_Datatype origin_dtype, int target_rank, MPI_Aint target_disp, int target_count, MPI_Datatype target_dtype, MPI_Win win);</code></li>
<li>request-based variants exist: <strong>MPI_R[xxx]</strong></li>
<li>no communicator, but MPI window object is used instead</li>
<li>all operations are <strong>non-blocking</strong></li>
</ul>
</li>
<li><strong>MPI_Accumulate</strong>
<ul>
<li><code>int MPI_Accumulate(const void *origin_addr, int origin_count, MPI_Datatype origin_dtype, int target_rank, MPI_Aint target_disp, int target_count, MPI_Datatype target_dtype, MPI_Op op, MPI_Win win);</code></li>
<li>atomic data aggregation</li>
<li>predefined operations only, element-wise atomic</li>
<li>predefined datatypes only</li>
</ul>
</li>
<li><strong>MPI_Get_accumulate</strong>
<ul>
<li><code>int MPI_Get_accumulate(const void *origin_addr, int origin_count, MPI_Datatype origin_datatype, void *result_addr, int result_count, MPI_Datatype result_datatype, int target_rank, MPI_Aint target_disp, int target_count, MPI_Datatype target_datatype, MPI_Op op, MPI_Win win);</code></li>
<li>returns the content of the target buffer <strong>before the accumulation</strong></li>
</ul>
</li>
<li><strong>MPI_Fetch_and_op</strong>
<ul>
<li><code>int MPI_Fetch_and_op(const void *origin_addr, void *result_addr, MPI_Datatype datatype, int target_rank, MPI_Aint target_disp, MPI_Op op, MPI_Win win);</code></li>
<li>a simplified version of <strong>MPI_Get_accumulate</strong></li>
</ul>
</li>
<li><strong>MPI_Compare_and_swap</strong>
<ul>
<li><code>int MPI_Compare_and_swap(const void *origin_addr, const void *compare_addr, void *result_addr, MPI_Datatype datatype, int target_rank, MPI_Aint target_disp, MPI_Win win);</code></li>
<li>compare values</li>
<li>if values match, swap, otherwise do nothing</li>
</ul>
</li>
</ul>
<h3 id="ordering-atomicity-completion">Ordering, Atomicity, Completion</h3>
<ul>
<li>completion
<ul>
<li>All RMA data transfer operations are non-blocking</li>
<li>can re-use the origin buffer only when the operation has locally completed</li>
<li><strong>local completion != remote completion</strong></li>
</ul>
</li>
<li>atomicity
<ul>
<li>only guaranteed for “<strong>accumulate</strong>” type operations, <strong>element-wise</strong></li>
</ul>
</li>
<li>ordering
<ul>
<li>only guaranteed for “<strong>accumulate</strong>” type operations on the same process</li>
<li>no ordering guaranteed for <strong>concurrent puts</strong> or <strong>concurrent puts &amp; gets</strong></li>
</ul>
</li>
</ul>
<h3 id="rma-epoch-model">RMA Epoch Model</h3>
<ul>
<li>access epoch
<ul>
<li>duration of time during which it may issue RMA operations</li>
</ul>
</li>
<li>exposure epoch
<ul>
<li>duration of time during which it may be the target of RMA operations</li>
</ul>
</li>
</ul>
<h3 id="active-target-synchronization-vs.-passive-target-synchronization">Active Target Synchronization vs. Passive Target Synchronization</h3>
<ul>
<li>active target
<ul>
<li>the target actively has to issue synchronization calls</li>
<li><strong>Fence</strong><br>
<img src="https://lh3.googleusercontent.com/Jxy5nuMz2jcp8NtJnN4nQtrIhJfXUBu0hoP_fH40s_RU4zE3R9TXk8Q5bAHit_bzZeMoWFobxcQ" alt="enter image description here">
<ul>
<li><code>int MPI_Win_fence(int assert, MPI_Win win);</code></li>
<li>collective call over the window object</li>
</ul>
</li>
<li><strong>PSCW</strong><br>
<img src="https://lh3.googleusercontent.com/diqd750Q7_wEnEPz9hhCW5e3xBBbiVHUnRsuis_aX3Ors-0rmNo5nVnlswa6SHZQ_s9OZD7pV98" alt="enter image description here">
<ul>
<li>post-start-complete-wait</li>
<li><code>int MPI_Win_post(MPI Group from_group, int assert, MPI Win win);</code></li>
<li><code>int MPI_Win_start(MPI Group to_group, int assert, MPI Win win);</code></li>
<li><code>int MPI_Win_complete(MPI Win win);</code></li>
<li><code>int MPI_Win_wait(MPI Win win);</code></li>
<li>more general than the fence model</li>
</ul>
</li>
</ul>
</li>
<li>passive target
<ul>
<li>target does not call any synchronization routines</li>
<li><strong>Lock</strong><br>
<img src="https://lh3.googleusercontent.com/2KNnedTdqysHFGIb4K2ZDsVFyV2e0CulZjiFsa1giNvHvyedLUN77SFNsQr9FSAUj1uCw4D4N80" alt="enter image description here">
<ul>
<li><code>int MPI_Win_lock(int lock_type, int rank, int assert, MPI Win win);</code></li>
<li><code>int MPI_Win_unlock(int rank, MPI Win win);</code></li>
<li>when <strong>MPI_Win_unlock</strong> returns, all <strong>RMA</strong> operations will have complete</li>
</ul>
</li>
<li><strong>Flush</strong><br>
<img src="https://lh3.googleusercontent.com/7EhBtEAs90c-JZ1ykzr7oGYPviE0Fv5AF80smSasoohiLzkfSw8GTKbOhCX2ZRMR4mZ7kvLPOKc" alt="enter image description here">
<ul>
<li>offers additional synchronization without closing the epoch</li>
<li><code>int MPI_Win_flush(int rank, MPI_Win win);</code>, local buffer can be reused after it returns, remote completion is guaranteed</li>
<li><code>int MPI_Win_flush_local(int rank, MPI_Win win);</code>, local buffer can be reused after it returns, remote completion is <strong>not</strong> guaranteed</li>
<li><code>int MPI_Win_flush_all(MPI_Win win);</code></li>
<li><code>int MPI_Win_flush_local_all(MPI_Win win);</code></li>
</ul>
</li>
</ul>
</li>
</ul>
<h3 id="scenarios">Scenarios</h3>
<ol>
<li><strong>MPI_Get</strong><br>
<img src="https://lh3.googleusercontent.com/CXAG3Lq7kDzDfOdlBjgD4QDI1OX36cYD8RZDmlIzqvPjhArZxtsGjR-zACKIrqUVNC72_q1MMeE" alt="enter image description here">
<blockquote>
<p>value of x is updated after the RMA is complete</p>
</blockquote>
</li>
<li><strong>MPI_Put</strong> =&gt; <strong>MPI_Get</strong><br>
<img src="https://lh3.googleusercontent.com/Mx4HA2PLWI4UjBcoSS8zDpvKf-SbcP8P9x0iBra_f93On2GcvaGzwHh66suTwLtcJ5THSrf4snI" alt="enter image description here">
<blockquote>
<p>results of concurrent puts or concurrent puts&amp;gets are <strong>undefined</strong></p>
</blockquote>
</li>
<li><strong>MPI_Get_accumulate</strong><br>
<img src="https://lh3.googleusercontent.com/sPVrzdPIVtY3-NUvOslfRWgIWtNrhJT9h_0V9MKStzkvcK0U4_OYb5VJGbR0Qoe64-4z_khDEac" alt="enter image description here">
<blockquote>
<p>ordering of <strong>accumulates</strong> is guaranteed, all RMAs will have complete after <strong>MPI_Win_unlock</strong> returns</p>
</blockquote>
</li>
<li><strong>MPI_Rget</strong><br>
<img src="https://lh3.googleusercontent.com/s4mloIBpNgSB7b5VjezNIO-tHaYjdIWVP12NmL3fOPlQgJUDb3Kz9C9bbweIOkODsh_jMCT-Wt8" alt="enter image description here">
<blockquote>
<p><strong>MPI_Rget</strong> is request-based, which guarantees RMA completion even before <strong>MPI_Win_unlock</strong></p>
</blockquote>
</li>
<li><strong>MPI_Put</strong> =&gt; <strong>MPI_Rget</strong><br>
<img src="https://lh3.googleusercontent.com/tSOfrHr-8ymcM2GD2OqA7QKITa-SjPWBsloM16DjJWUMYQzLysbj0XrPBUT4-H0rhp0yziXHyx8" alt="enter image description here">
<blockquote>
<p>the results of concurrent <strong>Rgets</strong>&amp;<strong>Rputs</strong> are also <strong>undefined</strong></p>
</blockquote>
</li>
</ol>

