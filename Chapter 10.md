---


---

<h1 id="chapter-10">Chapter 10</h1>
<h2 id="task-based-execution-in-openmp">Task-based Execution in OpenMP</h2>
<h3 id="task-based-execution">Task-based Execution</h3>
<ul>
<li>task
<ul>
<li><strong>units of work</strong> in a parallel program that can be executed independently of others</li>
<li>may have <strong>data dependences</strong> with other tasks</li>
</ul>
</li>
<li>OpenMP model for tasks
<ul>
<li>tasks are created when an OpenMP thread encounters a <strong>task constuct</strong></li>
<li>tasks are <strong>eventually executed</strong>:
<ul>
<li><strong>deferred</strong>: execution of tasks is independent of the generating of tasks</li>
<li><strong>undeferred</strong>: the generating of tasks is suspended until the undeferred task has completed</li>
</ul>
</li>
<li>task creation can be <strong>nested</strong></li>
</ul>
</li>
<li>OpenMP task directive
<ul>
<li><code>pragma omp task [clauses] \ structured-block</code></li>
</ul>
</li>
</ul>
<h3 id="task-synchronization">task synchronization</h3>
<ul>
<li>task synchronization points
<ul>
<li>after <strong>barriers</strong> (implicit or explicit)</li>
<li>after a <strong>taskwait</strong> construct
<ul>
<li>wait on completion of <strong>all child tasks of the current tasks</strong></li>
<li>via <code>#pragma omp taskwait</code></li>
<li>standalone directive, like <strong>barrier</strong></li>
<li>e.g.<br>
<img src="https://lh3.googleusercontent.com/W-tooETBCnrAKDNyiTh5umkiFXJ17nCRQ3jTJw43qUOQ-mVxvb1ABw33zG8-_WB6E_oMtBy3IQY" alt="enter image description here"></li>
</ul>
</li>
<li>after a <strong>taskgroup</strong> construct
<ul>
<li>wait on the completion of <strong>all child tasks and their descendants</strong></li>
<li>via <code>#pragma omp taskgroup \ structured-block</code></li>
<li>directive with an associated structured block</li>
<li>no guarantee for the completion of child tasks in the group, e.g.<br>
<img src="https://lh3.googleusercontent.com/UY1XZN95vUxUWvItVwCQN2wbtOtsQ0iNkJDNff_xrq_mfwD7lRd5--O_CgBYXYO4lPMLTrTbaSA" alt="enter image description here"></li>
<li>guarantee the completion of all tasks and their child tasks, e.g.<br>
<img src="https://lh3.googleusercontent.com/n8TlCRZ3W2gjDxpJyOX3vgSI371fhKMo472LE2pu9TYTf0y9kDHul2C0xCSW5iOaINApS5G_bp0" alt="enter image description here"></li>
</ul>
</li>
</ul>
</li>
<li>tied and untied tasks
<ul>
<li>visualization:<br>
<img src="https://lh3.googleusercontent.com/94aUCn3H-Oh2RXSxlDjTLo_XCKV377T5ky4tfUj3h_1XUQeLWkHom7_h6ttWcQT5tLIEQa20yEAA" alt="enter image description here"></li>
<li>for <strong>tied tasks</strong>, the <strong>same thread</strong> must resume execution after a task scheduling point
<ul>
<li>default</li>
</ul>
</li>
<li>for <strong>untied tasks</strong>, <strong>any thread</strong> in the team can resume execution after a task scheduling point
<ul>
<li>via <code>#pragma omp task untied</code></li>
</ul>
</li>
</ul>
</li>
</ul>
<h3 id="controlling-task-creation-and-execution">Controlling Task Creation and Execution</h3>
<ul>
<li>if the <strong>if clause</strong> is present and evaluates to <strong>false</strong>, an undeferred task is generated and immediately executed
<ul>
<li>can be used to avoid queueing tasks that are too small</li>
<li>child task are not affected</li>
<li>e.g.<br>
<img src="https://lh3.googleusercontent.com/1FF3PMt7LliTDHk3tFBBp8uGTPKG96Phtz73kwNRyPREmqeZQWAjRguwp6u7BJM96MxQNHW0UmkS" alt="enter image description here"></li>
</ul>
</li>
<li>if the <strong>final clause</strong> is present and evaluated to <strong>true</strong>, a regular task is generated and marked as “final”. if a final task is executed, all tasks constructs encounted will be final and <strong>included</strong>
<ul>
<li>can be also used to avoid queueing too small tasks</li>
<li>e.g.<br>
<img src="https://lh3.googleusercontent.com/gUPFt2aSq61Ye1WyKkNUQ-3FpvXiGJ_sCHU9L98nFe0YsAoK1wlWmNvVOuvFLXEZ-Ao7Ubh0_lt0" alt="enter image description here"></li>
</ul>
</li>
</ul>
<h3 id="data-dependencies-between-tasks">Data Dependencies Between Tasks</h3>
<ul>
<li>data dependencies can be formulated between tasks using the depend clause
<ul>
<li>only <strong>sibling</strong> tasks can have dependencies in OpenMP</li>
<li>via <code>#pragma omp task depend(dependence-type: list)</code></li>
</ul>
</li>
<li>dependence type:
<ul>
<li>in</li>
<li>out</li>
<li>inout(synonymous with out)</li>
<li>e.g.<br>
<img src="https://lh3.googleusercontent.com/UWU2NrUYGP8C_moA__ioUbRwcvS-GgzH3Tz2yRwonu35SsXTe59qZRyGIQsdNTK4zUmpqFnEzPem" alt="enter image description here"></li>
</ul>
</li>
</ul>

