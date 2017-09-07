
<html>
<head></font>
  <title>SIC/XE Instruction Set Summary</title></font>
<style type="text/css"></font>
  <!--</font>
  a{text-decoration:none}</font>
  a.usual:hover{color:red; background-color:#99FFFF; text-decoration: underline;}</font>
  a.bkcolor:hover{background-color:#99FFFF}</font>
  p.pagebreak{page-break-before: always}</font>
  --></font>
</style>
<!--
activator for a page break: <p class="pagebreak">
-->
  <link rel="shortcut icon" href="CW_small.ico">
</head>
<h2>SIC/XE Instruction Set</h2>
<font color="blue"><i>Op codes in blue are SIC/XE only instructions</i></font><br>
<font color="red"><i> Op codes in red are not implemented by the simulator</i></font>
<p>
Notes: P=privileged, C=CC set (<,=,>), <font color="red">F=floating point</font><br>
See Appendix A of <i>System Software</i> by Beck for information on instruction formats and addressing modes.
<pre>
Mnemonic     Format  Opcode  Effect                           Notes
-----------  ------  ------  -------------------------------  -----
ADD m          3/4     18    A &larr; (A) + (m..m+2)
<font color="red">ADDF m         3/4     58    F &larr; (F) + (m..m+5)                  F</font>
<font color="blue">ADDR r1,r2      2      90    r2 &larr; (r2) + (r1)</font>
AND m          3/4     40    A &larr; (A) &amp; (m..m+2)
<font color="blue">CLEAR r1        2       4    r1 &larr; 0</font>
COMP m         3/4     28    A : (m..m+2)                       C
<font color="red">COMPF m        3/4     88    F : (m..m+5)                       CF</font>
<font color="blue">COMPR r1,r2     2      A0    (r1) : (r2)                        C</font>
DIV m          3/4     24    A : (A) / (m..m+2)
<font color="red">DIVF m         3/4     64    F : (F) / (m..m+5)                  F</font>
<font color="blue">DIVR r1,r2      2      9C    (r2) &larr; (r2) / (r1)</font>
<font color="red">FIX             1      C4    A &larr; (F) [convert to integer]</font>
<font color="red">FLOAT           1      C0    F &larr; (A) [convert to floating]       F</font>
<font color="red">HIO             1      F4    Halt I/O channel number (A)       P</font>
J m            3/4     3C    PC &larr; m
JEQ m          3/4     30    PC &larr; m if CC set to =
JGT m          3/4     34    PC &larr; m if CC set to &gt;
JLT m          3/4     38    PC &larr; m if CC set to &lt;
JSUB m         3/4     48    L &larr; (PC); PC &larr; m<
LDA m          3/4     00    A &larr; (m..m+2)
<font color="blue">LDB m          3/4     68    B &larr; (m..m+2)</font>
LDCH m         3/4     50    A [rightmost byte] &larr; (m)
<font color="red">LDF m          3/4     70    F &larr; (m..m+5)                        F</font>
LDL m          3/4     08    L &larr; (m..m+2)
<font color="blue">LDS m          3/4     6C    S &larr; (m..m+2)</font>
<font color="blue">LDT m          3/4     74    T &larr; (m..m+2)</font>
LDX m          3/4     04    X &larr; (m..m+2)
<font color="red">LPS m          3/4     D0    Load processor status from        P</font>
<font color="red">                               information beginning at</font>
<font color="red">                               address m (see Section 6.2.1)</font>
<font color="blue">                               6.2.1)</font>
MUL m          3/4     20    A &larr; (A) * (m..m+2)
<font color="red">MULF m         3/4     60    F &larr; (F) * (m..m+5)</font>
<font color="blue">MULR r1,r2      2      98    r2 &larr; (r2) * (r1)</font>
<font color="red">NORM            1      C8    F &larr; (F) [normalized]                F</font>
OR m           3/4     44    A &larr; (A) | (m..m+2)
RD m           3/4     D8    A [rightmost byte] &larr; data         P
                               from device specified by (m)
<font color="blue">RMO r1,r2       2      AC    r2 &larr; (r1)</font>
RSUB           3/4     4C    PC &larr; (L)
<font color="blue">SHIFTL r1,n     2      A4    r1 &larr; (r1); left circular</font>
<font color="blue">                               shift n bits. [<i>for assembled</font>
<font color="blue">                               instruction, r2 is n-1</i>]</font>
<font color="blue">SHIFTR r1,n     2      A8    r1 &larr; (r1); right shift n bits</font>
<font color="blue">                               with vacated bit positions</font>
<font color="blue">                               set equal to leftmost</font>
<font color="blue">                               bit of (r1) [<i>for assembled</font>
<font color="blue">                               instruction, r2 is n-1</i>]</font>
<font color="red">SIO             1      F0    Start I/O channel number (A);     P</font>
<font color="blue">                               address of channel program</font>
<font color="blue">                               is given by (S)</font>
<font color="red">SSK m          3/4     EC    Protection key for address m      P</font>
<font color="blue">                               &larr; (A) (see Section 6.2.4)</font>
STA m          3/4     0C    m..m+2 &larr; (A)
<font color="blue">STB m          3/4     78    m..m+2 &larr; (B)</font>
STCH m         3/4     54    m &larr; (A) [rightmost byte]
<font color="red">STF m          3/4     80    m..m+5 &larr; (F)                        F</font>
<font color="red">STI m          3/4     D4    Interval timer value &larr;            P</font>
<font color="blue">                               (m..m+2) (see Section 6.2.1)</font>
STL m          3/4     14    m..m+2 &larr; (L)
<font color="blue">STS m          3/4     7C    m..m+2 &larr; (S)</font>
<font color="red">STSW m         3/4     E8    m..m+2 &larr; (SW)                     P</font>
<font color="blue">STT m          3/4     84    m..m+2 &larr; (T)</font>
STX m          3/4     10    m..m+2 &larr; (X)
SUB m          3/4     1C    A &larr; (A) - (m..m+2)
<font color="red">SUBF m         3/4     5C    F &larr; (F) - (m..m+5)                  F</font>
<font color="blue">SUBR r1,r2      2      94    r2 &larr; (r2) - (r1)</font>
<font color="red">SVC n           2      B0    Generate SVC interrupt. {<i>for
                               assembled instruction, r1 is n</i>]</font>
TD m           3/4     E0    Test device specified by (m)      PC
<font color="red">TIO             1      F8    Test I/O channel number (A)       PC</font>
TIX m          3/4     2C    X &larr; (X) + 1; (X) : (m..m+2)        C
<font color="blue">TIXR r1         2      B8    X &larr; (X) + 1; (X) : (r1)            C</font>
WD m           3/4     DC    Device specified by (m) &larr; (A)     P
                               [rightmost byte to device
                                specified by m]
</pre>
<p>
<h2>SIC/XE Instruction Formats</h2>
1 byte format
<!--
<table border="1"><tr>
<td width=8 align=center>0</td>
<td width=8 align=center>1</td>
<td width=8 align=center>2</td>
<td width=8 align=center>3</td>
<td width=8 align=center>4</td>
<td width=8 align=center>5</td>
<td width=8 align=center>6</td>
<td width=8 align=center>7</td>
</tr></table
-->
<table border="1"><tr>
<td width=106 align=center>op (8 bits)</td>
</tr></table>
2 byte format
<table border="1"><tr>
<td width=106 align=center>r1 (8 bits)</td>
<td width=106 align=center>r2 (8 bits)</td>
</tr></table>
3 byte format
<table border="1"><tr>
<td width=78 align=center>op (6 bits)</td>
<td width=8 align=center>n</td>
<td width=8 align=center>i</td>
<td width=8 align=center>x</td>
<td width=8 align=center>b</td>
<td width=8 align=center>p</td>
<td width=8 align=center>e</td>
<td width=156 align=center>disp (12 bits)</td>
</tr></table>
4 byte format
<table border="1"><tr>
<td width=78 align=center>op (6 bits)</td>
<td width=8 align=center>n</td>
<td width=8 align=center>i</td>
<td width=8 align=center>x</td>
<td width=8 align=center>b</td>
<td width=8 align=center>p</td>
<td width=8 align=center>e</td>
<td width=262 align=center>address (20 bits)</td>
</tr></table>
<p>
<h2>Working registers</h2>
<pre>
Register Number
-------- ------
    A      0
    X      1
    L      2
    B      3
    S      4
    T      5
    F      6
</pre>
<p>
<h2>3 and 4 Byte Addressing Modes</h2>
The target address determined by the addressing mode locates the instruction operand<br>
<font color=red>nixbpe settings not specified cause machine exceptions</font><br>
<font color="blue">4-byte settings are high-lighted in blue</font>, <font color="green">simple SIC in green</font>
<pre>
Addressing  Flag bits     Description
Mode        n i x b p e
-------------------------------------
Direct      1 1 0 0 0 0   12 bit displacement is target address
<font color="blue">            1 1 0 0 0 1   20 bit address is target address</font>
            1 1 0 0 1 0   12 bit 2's complement displacement from PC (PC relative)
            1 1 0 1 0 0   12 bit base unsigned displacement forward from B (base displacement)
            1 1 1 0 0 0   index register X added to direct address to get target address
<font color="blue">            1 1 1 0 0 1   index register X added to direct address to get target address</font>
            1 1 1 0 1 0   index register X added to PC relative computation to get target address
            1 1 1 1 0 0   index register X added to base displacement computation to get target address
<font color="green">            0 0 0 - - -   simple SIC instruction, last 15 bits are the address</font>
<font color="green">            0 0 1 - - -   index register X added to direct address to get target address</font>
Indirect    1 0 0 0 0 0   Computed memory address contains the target address
<font color="blue">            1 0 0 0 0 1   Computed memory address contains the target address</font>
            1 0 0 0 1 0   Computed memory address contains the target address
            1 0 0 1 0 0   Computed memory address contains the target address
Immediate   0 1 0 0 0 0   Computed memory address is the operand (target address is the instruction)
<font color="blue">            0 1 0 0 0 1   Computed memory address is the operand (target address is the instruction)</font>
            0 1 0 0 1 0   Computed memory address is the operand (target address is the instruction)
            0 1 0 1 0 0   Computed memory address is the operand (target address is the instruction)
</pre>
<font color="red">NOTE: indexed addressing is not supported for Indirect and Immediate addressing modes</font>
<p>
<br>
</body>
</html>
