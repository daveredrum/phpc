---


---

<h1 id="chapter-1">Chapter 1</h1>
<h2 id="gpus-and-cuda-programming">GPUs and CUDA Programming</h2>
<h3 id="terminology">Terminology</h3>
<ul>
<li><strong>GPU</strong> (Graphic Processing Unit)</li>
<li><strong>CUDA</strong> (Compute Unified Device Architecture)</li>
<li>a GPU (the <strong>device</strong>) is attached to the machine (the <strong>host</strong>) via PCI express (<strong>PCIe</strong>)</li>
<li>functions executed on the GPU are called <strong>kernels</strong></li>
<li><strong>__global__</strong> and <strong>__device__</strong> decoration in CUDA signifies that a function or variable is to be executed on the device</li>
<li>function qualifiers
<ul>
<li><strong>__global__</strong>:
<ul>
<li>executed on GPU, invoked from within host code</li>
<li>cannot be called from device code</li>
<li>must return void</li>
</ul>
</li>
<li><strong>__device__</strong>
<ul>
<li>executed on GPU, called from other GPU functions</li>
<li>cannot be called from host code</li>
</ul>
</li>
<li><strong>__host__</strong>
<ul>
<li>can only be executed by CPU, called from host</li>
</ul>
<blockquote>
<p><strong>__host__</strong> and <strong>__device__</strong> can be combined</p>
</blockquote>
</li>
</ul>
</li>
<li>scheduing
<ol>
<li>GPU schedules thread blocks for execution on a <strong>streaming multiprocessor (SM)</strong></li>
<li>a SM schedules a SIMD thread (warp) for execution on a <strong>streaming processor (SP)</strong></li>
</ol>
<blockquote>
<p>scheduling is done in <strong>hardware</strong></p>
</blockquote>
</li>
</ul>
<h3 id="host-device-kernel">Host, Device, Kernel</h3>
<ul>
<li>visualization<br>
<img src="https://lh3.googleusercontent.com/hnwEx8gc9GgsGUv6jJYla8AdA8oTZ7_2HDkb_WyUQ4JXG0xAfy2UqO9qaTDE1-FM24I1hXZ8KK5w" alt="enter image description here"></li>
<li>an example for a CUDA kernel<br>
<img src="https://lh3.googleusercontent.com/P9wES0Z--5ln5od8IT49tcK3TtKm1H2IUpE2MKgZrvRGCqVYfMOLBAUXo8obh2Uq5NmvYYrOEDs5" alt="enter image description here"></li>
</ul>
<h3 id="cuda-development-toolchain">CUDA Development Toolchain</h3>
<ul>
<li>visualization:<br>
<img src="https://lh3.googleusercontent.com/aLq09zwRP0pNfNFDOVNn9m-PmRmDYtlVLYBuUaT4m_Xy_kMBohIsBn1hR6yUC5xHE7H7zlaqUI2o" alt="enter image description here"></li>
<li>the <strong>NVCC</strong> compiler creates both GPU and CPU code
<ul>
<li><strong>PTX</strong> is created for the GPU</li>
</ul>
</li>
<li><strong>PTX</strong> assembly instructions
<ul>
<li>translated to GPU binaries by the graphics driver</li>
</ul>
<blockquote>
<p><strong>PTX</strong>: Parallel Thread Execution</p>
</blockquote>
</li>
</ul>
<h3 id="cuda-execution-hierarchy">CUDA Execution Hierarchy</h3>
<ul>
<li>visualization:<br>
<img src="https://lh3.googleusercontent.com/_JqY8eds78V_WHwnTqb3Y0NApxsIKNlweTCctK4_W7aRvK93FFxLR1FkBBm_vJNrGiUkNBziKk2W" alt="enter image description here"></li>
<li>a <strong>stream</strong> is a list of <strong>grids</strong> that execute in-order</li>
<li>a <strong>grid</strong> consists of up to <span class="katex--inline"><span class="katex"><span class="katex-mathml"><math><semantics><mrow><msup><mn>2</mn><mrow><mn>3</mn><mn>2</mn></mrow></msup></mrow><annotation encoding="application/x-tex">2^{32}</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="strut" style="height: 0.814108em;"></span><span class="strut bottom" style="height: 0.814108em; vertical-align: 0em;"></span><span class="base"><span class="mord"><span class="mord mathrm">2</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height: 0.814108em;"><span class="" style="top: -3.063em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mathrm mtight">3</span><span class="mord mathrm mtight">2</span></span></span></span></span></span></span></span></span></span></span></span></span> <strong>thread blocks</strong></li>
<li>a <strong>thread block</strong> consists of up to 1024 CUDA threads</li>
<li>a <strong>CUDA thread</strong> is a scalar execution context
<ul>
<li>groups of 32 threads form a <strong>warp</strong> or SIMD thread</li>
</ul>
</li>
<li>a <strong>warp</strong> is executed in lockstep</li>
</ul>

