---
layout: post
title:  "Some Frequency Estimation Algorithms"
date:   2007-03-21
tags: algorithm
---
from: [Frequency Algorithms](https://sites.google.com/site/kootsoop/frequency-algorithms)

<table border="0" bordercolor="#111111" cellpadding="0" cellspacing="0" style="border-collapse:collapse" width="750">
<tbody>
<tr>
<td width="284"><font color="#008000" face="Arial" size="4">Algorithm
Type</font></td>
<td width="251"><font color="#008000" face="Arial" size="4">Matlab
Code Links</font></td>
<td width="92"><font color="#008000" face="Arial" size="4"> Complexity</font></td>
<td width="123"><font color="#008000" face="Arial" size="4">Statistically</font><font face="Arial" size="4"> </font> <font color="#008000" face="Arial" size="4">Efficient?</font></td>
</tr>
<tr>
<td bgcolor="#c0c0c0" rowspan="3" width="284"> <font color="#000000" face="Arial" size="2">Maximum Likelihood (ML) &amp;
Approximate ML</font></td>
<td bgcolor="#c0c0c0" width="251"> <font color="#000000" face="Arial" size="2">Maximum Likelihood</font></td>
<td bgcolor="#c0c0c0" width="92"><font face="Arial" size="2">&gt;
O(T log T)</font></td>
<td bgcolor="#c0c0c0" width="123"> <font color="#000000" face="Arial" size="2">Yes</font></td>
</tr>
<tr>
<td bgcolor="#c0c0c0" width="251"> <font color="#000000" face="Arial" size="2">Periodogram Maximiser</font></td>
<td bgcolor="#c0c0c0" width="92"><font face="Arial" size="2">&gt;
O(T log T)</font></td>
<td bgcolor="#c0c0c0" width="123"> <font color="#000000" face="Arial" size="2">Yes</font></td>
</tr>
<tr>
<td bgcolor="#c0c0c0" width="251"> <font color="#000000" face="Arial" size="2"><a href="https://sites.google.com/site/kootsoop/frequency-algorithms/discperiod">Discrete-frequency
Periodogram Maximizer</a> </font></td>
<td bgcolor="#c0c0c0" width="92"><font face="Arial" size="2"> O(T
log T)</font></td>
<td bgcolor="#c0c0c0" width="123"> <font color="#000000" face="Arial" size="2">No</font></td>
</tr>
<tr>
<td width="284"><font color="#000000" face="Arial" size="2">Fourier
Coefficient</font></td>
<td width="251"><font color="#000000" face="Arial" size="2"><a href="https://sites.google.com/site/kootsoop/frequency-algorithms/ericj">Interpolation Techniques</a> supplied by Eric
Jacobsen, EF Data Corp (now Intel).</font>
<p> <font face="Arial" size="2">Some extra work done by Eric is
available <a href="http://www.ericjacobsen.org/fe.htm" rel="nofollow">here</a>
(or mirrored <a href="https://sites.google.com/site/kootsoop/frequency-algorithms/ericj2">here</a>).</font></p>
</td>
<td width="92"><font face="Arial" size="2">O(T log T) </font> </td>
<td width="123"><font color="#000000" face="Arial" size="2">No</font><font face="Arial" size="2"> </font> </td>
</tr>
<tr>
<td bgcolor="#c0c0c0" rowspan="2" width="284"> <font color="#000000" face="Arial" size="2">Signal Subspace</font></td>
<td bgcolor="#c0c0c0" width="251"><font color="#000000" face="Arial" size="2">Minimum Variance</font><font face="Arial" size="2"> </font> </td>
<td bgcolor="#c0c0c0" width="92"><font face="Arial" size="2">O(T<sup><b>3</b></sup>)
      </font> </td>
<td bgcolor="#c0c0c0" width="123"><font color="#000000" face="Arial" size="2">No</font><font face="Arial" size="2"> </font> </td>
</tr>
<tr>
<td bgcolor="#c0c0c0" width="251"><font color="#000000" face="Arial" size="2">Bartlett</font><font face="Arial" size="2"> </font>
</td>
<td bgcolor="#c0c0c0" width="92"><font face="Arial" size="2">O(T<sup><b>3</b></sup>)
      </font> </td>
<td bgcolor="#c0c0c0" width="123"><font color="#000000" face="Arial" size="2">No</font><font face="Arial" size="2"> </font> </td>
</tr>
<tr>
<td rowspan="2" width="284"><font color="#000000" face="Arial" size="2">Noise Subspace</font></td>
<td width="251"><font color="#000000" face="Arial"><a href="https://sites.google.com/site/kootsoop/frequency-algorithms/pisarenko"> <font size="2">Pisarenko</font></a></font><font face="Arial" size="2"> </font> </td>
<td width="92"><font face="Arial" size="2">O(T) </font> </td>
<td width="123"><font color="#000000" face="Arial" size="2">No</font><font face="Arial" size="2"> </font> </td>
</tr>
<tr>
<td width="251"><font color="#000000" face="Arial" size="2">MUSIC</font><font face="Arial" size="2"> </font> </td>
<td width="92"><font face="Arial" size="2">O(T<sup><b>3</b></sup>)
      </font> </td>
<td width="123"><font color="#000000" face="Arial" size="2">No</font><font face="Arial" size="2"> </font> </td>
</tr>
<tr>
<td bgcolor="#c0c0c0" width="284"> <font color="#000000" face="Arial" size="2">Phase Weighted Averagers</font></td>
<td bgcolor="#c0c0c0" width="251">
<p><font color="#000000" face="Arial"><a href="https://sites.google.com/site/kootsoop/frequency-algorithms/wlp" style="color:rgb(0,0,255)"> <font size="2">Lank-Reed-Pollon,
Kay, Lovell-Williamson, Clarkson-Kootsookos-Quinn</font></a></font><font face="Arial" size="2"> </font> </p>
</td>
<td bgcolor="#c0c0c0" width="92"><font face="Arial" size="2">O(T)
      </font> </td>
<td bgcolor="#c0c0c0" width="123"><font color="#000000" face="Arial" size="2">Depends on technique. Most No.</font><font face="Arial" size="2"> </font> </td>
</tr>
<tr>
<td rowspan="4" width="284"><font color="#000000" face="Arial" size="2">Filtering Techniques</font></td>
<td width="251"><font color="#000000" face="Arial"><font size="2">Fernandes-Goodwin-de
Souza</font></font><font face="Arial" size="2"> </font> </td>
<td width="92"><font color="#000000" face="Arial"><font size="2">O(T)</font></font><font face="Arial" size="2"> </font> </td>
<td width="123"><font color="#000000" face="Arial" size="2">Yes</font><font face="Arial" size="2"> </font> </td>
</tr>
<tr>
<td width="251"><font color="#000000" face="Arial"><a href="https://sites.google.com/site/kootsoop/frequency-algorithms/qnf">
<font size="2">Quinn-Fernandes</font></a></font><font face="Arial" size="2"> </font> </td>
<td width="92"><font color="#000000" face="Arial"><font size="2">O(T)</font></font><font face="Arial" size="2"> </font> </td>
<td width="123"><font color="#000000" face="Arial" size="2">Yes</font><font face="Arial" size="2"> </font> </td>
</tr>
<tr>
<td width="251"><font color="#000000" face="Arial"><font size="2">Hannan-Huang</font></font><font face="Arial" size="2"> </font> </td>
<td width="92"><font color="#000000" face="Arial" size="2">?</font><font face="Arial" size="2"> </font> </td>
<td width="123"><font color="#000000" face="Arial" size="2">?</font><font face="Arial" size="2"> </font> </td>
</tr>
<tr>
<td width="251"><font color="#000000" face="Arial"><font size="2">Nehorai-Porat</font></font><font face="Arial" size="2"> </font> </td>
<td width="92"><font color="#000000" face="Arial" size="2">?</font><font face="Arial" size="2"> </font> </td>
<td width="123"><font color="#000000" face="Arial" size="2">?</font><font face="Arial" size="2"> </font> </td>
</tr>
</tbody>
</table>
<table border="0" bordercolor="#111111" cellpadding="0" cellspacing="0" height="43" style="border-collapse:collapse" width="750">
<tbody>
