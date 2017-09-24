
<html>

<h2>SIC/XE Instruction Set</h2>
<font color="blue"><i>Op codes in blue are SIC/XE only instructions</i></font><br>
<font color="red"><i> Op codes in red are not implemented by the simulator</i></font>
<p>
Notes: P=privileged, C=CC set (<,=,>), <font color="red">F=floating point</font><br>
See Appendix A of <i>System Software</i> by Beck for information on instruction formats and addressing modes.
<pre>
Mnemonic     Format  Opcode  Effect                           Notes
-----------  ------  ------  -------------------------------  -----
ADD m          3/4     18    A ← (A) + (m..m+2)                   Adds onto the accumulator. 
ADDF m         3/4     58    F ← (F) + (m..m+5)                 F Adds a float to the float accumulator. 
ADDR r1,r2      2      90    r2 ← (r2) + (r1)                     Adds two reg together. 
AND m          3/4     40    A ← (A) & (m..m+2)                   We havent gone over it but it looks like it takes contents from accumulator and adds it to the beginning of the word.
CLEAR r1        2       4    r1 ← 0                               Clears reg and seems to set it to zero.
COMP m         3/4     28    A : (m..m+2)                       C Compares the acumulator to specified word.
COMPF m        3/4     88    F : (m..m+5)                       CFCompares two float points. 
COMPR r1,r2     2      A0    (r1) : (r2)                        C Compares reg.
DIV m          3/4     24    A : (A) / (m..m+2)                   Divide accumulator by word (looks like).
DIVF m         3/4     64    F : (F) / (m..m+5)                 F Divide float.
v. pro tip (with division and subtraction it does make a difference the format on dividing registries.)
DIVR r1,r2      2      9C    (r2) ← (r2) / (r1)                   Divide Registries ... (this is important you have to keep the same format).
FIX             1      C4    A ← (F) [convert to integer]         converts from an float to an integer.
FLOAT           1      C0    F ← (A) [convert to floating]      F converts and integer to a float.
HIO             1      F4    Halt I/O channel number (A)        P 
J m            3/4     3C    PC ← m                               jumps to the loop you set it to without setting a cc.
JEQ m          3/4     30    PC ← m if CC set to =                jumps to the loop and it creates the cc for less than.=
JGT m          3/4     34    PC ← m if CC set to >                jumps to the loop and it creates the cc for less than.>
JLT m          3/4     38    PC ← m if CC set to <                jumps to the loop and it creates the cc for less than.
JSUB m         3/4     48    L ← (PC); PC ← m<                    jump subroutine ... jump to the subroutine sets the cc.
LDA m          3/4     00    A ← (m..m+2)                         load the accumulator.
LDB m          3/4     68    B ← (m..m+2)                         load the base registry.
LDCH m         3/4     50    A [rightmost byte] ← (m)             load the character a character uses generic registry.
LDF m          3/4     70    F ← (m..m+5)                       F load the floatpoint registry .... a float has its own registry.
LDL m          3/4     08    L ← (m..m+2)                         loading to the loader.
LDS m          3/4     6C    S ← (m..m+2)                         
LDT m          3/4     74    T ← (m..m+2)                         
LDX m          3/4     04    X ← (m..m+2)                         loading into the X registry ... 
LPS m          3/4     D0    Load processor status from         P 
                               information beginning at
                               address m (see Section 6.2.1)
                               6.2.1)
MUL m          3/4     20    A ← (A) * (m..m+2)                   Multiply.
MULF m         3/4     60    F ← (F) * (m..m+5)                   Multiply Floater Pointer.
MULR r1,r2      2      98    r2 ← (r2) * (r1)                     Multiply Register.
NORM            1      C8    F ← (F) [normalized]               F 
OR m           3/4     44    A ← (A) | (m..m+2)
RD m           3/4     D8    A [rightmost byte] ← data          P
                               from device specified by (m)
RMO r1,r2       2      AC    r2 ← (r1)                            
RSUB           3/4     4C    PC ← (L)                             Return Subroutine.
SHIFTL r1,n     2      A4    r1 ← (r1); left circular            
                               shift n bits. [for assembled
                               instruction, r2 is n-1]
SHIFTR r1,n     2      A8    r1 ← (r1); right shift n bits       
                               with vacated bit positions
                               set equal to leftmost
                               bit of (r1) [for assembled
                               instruction, r2 is n-1]
SIO             1      F0    Start I/O channel number (A);      P
                               address of channel program
                               is given by (S)
SSK m          3/4     EC    Protection key for address m       P 
                               ← (A) (see Section 6.2.4)
STA m          3/4     0C    m..m+2 ← (A)                         store the accumulator.
STB m          3/4     78    m..m+2 ← (B)                         store the base register.
STCH m         3/4     54    m ← (A) [rightmost byte]             store the character.
STF m          3/4     80    m..m+5 ← (F)                       F store the float point.
STI m          3/4     D4    Interval timer value ←             P store the index. (definately or kill vasquez)🤖
                               (m..m+2) (see Section 6.2.1)       
STL m          3/4     14    m..m+2 ← (L)                         store loader.
STS m          3/4     7C    m..m+2 ← (S)                         
STSW m         3/4     E8    m..m+2 ← (SW)                      P 
STT m          3/4     84    m..m+2 ← (T)                         
STX m          3/4     10    m..m+2 ← (X)                          
SUB m          3/4     1C    A ← (A) - (m..m+2)                    subtracting ... from sic.
SUBF m         3/4     5C    F ← (F) - (m..m+5)                 F  subtract float.
SUBR r1,r2      2      94    r2 ← (r2) - (r1)                      subtract two registries from each other.
SVC n           2      B0    Generate SVC interrupt. {for
                               assembled instruction, r1 is n]
TD m           3/4     E0    Test device specified by (m)       PC
TIO             1      F8    Test I/O channel number (A)        PC
TIX m          3/4     2C    X ← (X) + 1; (X) : (m..m+2)        C
TIXR r1         2      B8    X ← (X) + 1; (X) : (r1)            C
WD m           3/4     DC    Device specified by (m) ← (A)      P
                               [rightmost byte to device
                                specified by m]
</pre>

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
<td width=106 align=center>op (6 bits)</td>
<td width=8 align=center>n</td>
<td width=8 align=center>i</td>
<td width=8 align=center>x</td>
<td width=8 align=center>b</td>
<td width=8 align=center>p</td>
<td width=8 align=center>e</td>
<td width=106 align=center>disp (12 bits)</td>
</tr></table>
4 byte format
<table border="1"><tr>
<td width=106 align=center>op (6 bits)</td>
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
