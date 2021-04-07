
  <div id="header">
      <div id="header-right"><div style="float:right;width:100%;text-align:right;"><font color="grey" style="font-size:x-large;"><font color="#852339"><b>Motivation</b></font><br>
      Processing Steps<br>
      Results</font></div></div>
  </div>
<h2> GPGPU Programming </h2>
<div align="left" style="padding-top:5%;width:40%;float:right;">
<img alt="wwu-logo" style="float:right;width:100%;padding-top:15%;" data-src="images/MA_figures/comparisongpucpu.svg">
</div>
<div align="left" style="padding-left:0%;padding-top:5%;width:55%;float:left;">

<h3>Distinct problems require different solution approaches</h3>
<ul>
<li> CPU </li>
<ul>
<li> Communication intensive Tasks </li>
<li> Control flow is important </li>
</ul>
<li>GPU</li>
<ul>
<li>Little amount of communication
<li>High Data Rates
<li> Single Instruction Multiple Threads (SIMT)</li>
  </ul>
  </ul>
</div>

---


  <div id="header">
      <div id="header-right"><div style="float:right;width:100%;text-align:right;"><font color="grey" style="font-size:x-large;"><font color="#852339"><b>Motivation</b></font><br>
      Processing Steps<br>
      Results</font></div></div>
  </div>
<h2> High- and Low-Level Approaches </h2>

<div style="float:left;width:50%;">
	<h3 style="text-transform: capitalize;color:black;text-align:left;"> Low-Level-Approach</h3>
	<h5 style="text-transform: capitalize;color:green;text-align:left;font-weight:normal;padding:20px 0 20px 0;"> &#10004; Fine-grained optimization</h5>
	<h5 style="text-transform: capitalize;color:#a20101;text-align:left;font-weight:normal;padding:20px 0 20px 0;"> &#10006; Expertise required</h5>
<h5 style="text-transform: capitalize;color:#a20101;text-align:left;font-weight:normal;padding:20px 0 20px 0;">&#10006; High implementation effort</h5>
<div class="fragment">
	<div style="text-align:left;background-color:black; color:white;font-family: Andale Mono,AndaleMono,monospace;font-size: 20pt;padding-left:5pt;padding-top:3pt;border-radius: 5px;">
	<font color="grey">1 </fonts> <font color="#4EC9B0">int</font> size = 42;<br>
	 <font color="grey">2 </font> <font color="#4EC9B0">float\*</font> d_input;<br>
	 <font color="grey">3 </font> <font color="#4EC9B0">float\*</font> h_input = <font color="#569CD6">malloc</font>(size \* <font color="#4EC9B0">sizeof</font>(<font color="#4EC9B0">float</font>));<br>
	 <font color="grey"> 4 </font> <font color="#D69D85">cudaMalloc</font> (&d_input, size \* <font color="#4EC9B0">sizeof</font>(<font color="#4EC9B0">float</font>));<br>
	<font color="grey">5 </font> <font color="#D69D85">cudaMemcpy</font> (&d_input, h_input \* <font color="#4EC9B0">sizeof</font>(<font color="#4EC9B0">float</font>));<br>
 </div>
 </div>
 </div>
	<div style="float:right;width:45%;margin-left:3pt;">
		<div class="fragment">			<h3 style="text-transform: capitalize;color:black;text-align:left;">  High-Level-Approach</h3>

			<h5 style="text-transform: capitalize;color:green;text-align:left;font-weight:normal;padding:20px 0 20px 0;"> &#10004; Usability</h5>
			<h5 style="text-transform: capitalize;color:green;text-align:left;font-weight:normal;padding:20px 0 20px 0;"> &#10004; Maintainability</h5>
			<h5 style="text-transform: capitalize;color:green;text-align:left;font-weight:normal;padding:20px 0 20px 0;"> &#10004; Transferability</h5>
			<h5 style="text-transform: capitalize;color:#cb9f01;text-align:left;font-weight:normal;padding:20px 0 20px 0;">? Performance Losses</h5>
		</div>
		<div class="fragment">
			<div style="text-align:left;background-color:black; color:white;font-family: Andale Mono,AndaleMono,monospace;font-size: 20pt;padding-left:5pt;padding-top:3pt;border-radius: 5px;">
	 			<font color="grey">1</font> <font color="#569CD6">array</font>&lt;<font color="#4EC9B0">float</font>,42,dist&gt; input;
 			</div>
		</div>
    </div>

---

<div id="header">
    <div id="header-right"><div style="float:right;width:100%;text-align:right;"><font color="grey" style="font-size:x-large;"><font color="#852339"><b>Motivation</b></font><br>
    Processing Steps<br>
    Results</font></div></div>
</div>
<h2> Motivation - Telescope Data</h2>
<img alt="wwu-logo" style="float:right;width:30%;" data-src="images/MA_figures/telescope.jpg">

<div align="left" style="padding-left:5%;width:60%;">

* Telescope Processing requires tremendous amount of data
* Max Planck Institut for Radio Astronomy (MPIfR) has multiple telescopes
  * Next generation <span class="highlight" style="color:#852339;">**5 PB/s**</span>
  * Effelsberg telescope <span class="highlight" style="color:#852339;">**256 GB/s**</span> <br>
* PFB to process data <!-- .element: class="fragment" data-fragment-index="1" -->
  * Exemplary process
<img alt="wwu-logo" style="float:right;" data-src="images/MA_figures/process-1.png">
