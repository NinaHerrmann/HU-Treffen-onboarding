<div id="header">
    <div id="header-right"><div style="float:right;width:100%;text-align:right;"><font color="grey" style="font-size:x-large;">Motivation<br>
    <font color="#852339"><b>Processing Steps</b></font><br>
    Results</font></div></div>
</div>
# Implementation
<div align="left" style="padding-left:5%;width:45%;float:left;">
<h3>Low-Level implementation</h3>
<h5>FIR-Filter:</h5>
<img alt="wwu-logo" style="width:80%;" data-src="images/MA_figures/blockoverlap.jpg">
<h5> DFT:</h5>
<ul><li>cuFFT library</li></ul>
</div>
<div align="left" style="width:50%;float:right;"><br style="line-width:50%;"> <!-- .element: class="fragment" data-fragment-index="1" -->
<h3>High-Level implementation</h3>
<ul><li>FIR-filter:</li>
<div style="text-align:left;background-color:black; color:white;font-family: Andale Mono,AndaleMono,monospace;font-size: 16pt;padding-left:5pt;padding-top:3pt;border-radius: 5px">
  <font color="grey">1</font><font color="#4EC9B0"> float</font> <font color="#569CD6">FIR</font>(<font color="#4EC9B0">int</font> taps, <font color="#4EC9B0">int</font> channels, <font color="#4EC9B0">int</font> spectra, <font color="#4EC9B0">int</font> Index, <font color="#4EC9B0">float</font> a) {<br>
  <font color="grey">2</font> &nbsp;<font color="#4EC9B0">float</font> newa = 0;<br>
  <font color="grey">3</font>	&nbsp;for (<font color="#4EC9B0">int</font> j = 0; j < taps; j++) {<br>
  <font color="grey">4</font>	&nbsp;&nbsp;<font color="#4EC9B0">int</font> offset = Index+(j\*channels);<br>
  <font color="grey">4</font>	&nbsp;&nbsp;newa += input[offset] \* coeff[offset%(taps\*channels)];<br>
  <font color="grey">5</font>	&nbsp;}<br>
  <font color="grey">6</font>	&nbsp;return newa;<br>
  <font color="grey">7</font>}
  </div> <br>
<div style="text-align:left;background-color:black; color:white;font-family: Andale Mono,AndaleMono,monospace;font-size: 16pt;padding-left:5pt;padding-top:3pt;border-radius: 5px">
  <font color="grey">1</font> input_double.<font color="#D69D85">mapIndexInPlace</font>(<font color="#569CD6">FIR</font>(taps, channels, spectra));<br>
</div><br>
<li>DFT - FFT Algorithm:</li>
<div style="text-align:left;background-color:black; color:white;font-family: Andale Mono,AndaleMono,monospace;font-size: 17pt;padding-left:5pt;padding-top:3pt;border-radius: 5px">
  <font color="grey">1 </font> <font color="#4EC9B0">for</font>(<font color="#4EC9B0">int</font> j=0; j &lt; log2size; j++) {<br>
  <font color="grey">2 &nbsp;</font> c_input_double.<font color="#D69D85">mapIndexInPlace</font>(fetch(j, log2size));<br>
  <font color="grey">3 &nbsp;</font> c_output.<font color="#D69D85">mapIndexInPlace</font>(combine(j, log2size, PI, 16));<br>
  <font color="grey">4</font>}
</div>
</ul>
