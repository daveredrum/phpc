---


---

<h1 id="chapter-5">Chapter 5</h1>
<h2 id="distributed-memory-machines">Distributed Memory Machines</h2>
<h3 id="properties-of-interconnection-nerworks">Properties of Interconnection Nerworks</h3>
<ul>
<li>early distributed memory machines
<ul>
<li>a collection of <strong>microprocessors</strong></li>
<li>communications was performed via <strong>bidirectional queues</strong> between nearest neighbors</li>
<li>a strong emphasis on <strong>topology</strong> in algorithms</li>
</ul>
</li>
<li>modern distributed memory machines
<ul>
<li>nodes with processor and memory</li>
<li>network interface
<ul>
<li>Communication Agent (<strong>CA</strong>) processes the messages</li>
</ul>
</li>
<li>scalable interconnection network</li>
<li>characteristics
<ul>
<li><strong>topology</strong>: how the nodes are connected</li>
<li><strong>latency</strong>: how long to get between nodes in the network</li>
<li><strong>bandwidth</strong>: how much data can be moved per unit time</li>
</ul>
</li>
<li>design characteristics
<ul>
<li>routing algorithm</li>
<li>switching strategy
<ul>
<li><strong>circuit switching</strong>: full path reserved for entire message</li>
<li><strong>packet switching</strong>: message broken into separately-routed packets</li>
</ul>
</li>
<li>flow control</li>
</ul>
</li>
</ul>
</li>
</ul>
<h3 id="performance-properties-of-networks">Performance Properties of Networks</h3>
<ul>
<li>
<p><strong>diameter</strong></p>
<ul>
<li>the maximum of the shortest path between a pair of nodes</li>
</ul>
</li>
<li>
<p><strong>latency</strong></p>
<ul>
<li>delay between send and receive times</li>
<li><strong>hardware latencies</strong></li>
<li><strong>software latencies</strong></li>
</ul>
</li>
<li>
<p><strong>bandwidth</strong></p>
<ul>
<li><em>bandwidth (of a link) = num_wires * bit_per_second</em></li>
</ul>
</li>
<li>
<p><strong>bisection bandwidth</strong><br>
<img src="https://lh3.googleusercontent.com/Z07VAZ4FPP1lFUHHGw20bEeezLbiW6lyFRiRnZOkr-B6vlzXKTP9I8JvG-BxJ_wv7M-G6fhxV4s" alt="bandwidth across the smallest cut that divides network into two equal halves"></p>
<ul>
<li>bandwidth across the smallest cut that divides network into two equal halves</li>
</ul>
</li>
<li>
<p><strong>Network Topologies</strong></p>
<ul>
<li>fully connected
<ul>
<li>bus</li>
<li>crossbar</li>
</ul>
</li>
<li>ring</li>
<li>linear array</li>
<li>two dimensional mesh</li>
<li>two dimensional torus</li>
<li>hypercubes
<ul>
<li>routing: <strong>Greycode addressing</strong>, each node connected to d others with 1 bit different</li>
</ul>
</li>
<li>tree
<ul>
<li>diameter: <em>2logn</em></li>
</ul>
</li>
<li>fat tree
<ul>
<li>more links near the top</li>
</ul>
</li>
</ul>
</li>
</ul>
<h3 id="communication-performance-models">Communication Performance Models</h3>
<ul>
<li>latency and bandwidth model
<ul>
<li><strong>time = alpha + n*beta</strong>, where alpha = latency, beta = 1/bandwidth</li>
<li>one long message is cheaper than many short ones</li>
</ul>
</li>
</ul>

