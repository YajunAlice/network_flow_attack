# Texas A&M University

<p align="center">
  <b>Maintained by: Lang Feng, Yujie Wang, Jiang Hu and Jeyavijayan (JV) Rajendran</b><br>
  <b>Contact: flwave@tamu.edu, tjwangyj@hotmail.com, jianghu@tamu.edu and jv.rajendran@tamu.edu</b><br>
</p>

+++++11/04/2017: Fixed the bug which makes the output netlist the same as the original netlist.<br>
+++++11/16/2017: version 1.3: 1. Fixed the bug which will cause crash in some cases; 2. Modified the format of output netlist file for easier parsing.<br>
+++++04/30/2018: Fixed the bug that the program cannot recognize the primary input/output at metal 10.<br>

Split fabrication is a technique to prevent an untrusted foundry from reverse engineering the design. It entails separating the design into front-end-of-line (FEOL) and back-end-of-line (BEOL)  parts and manufacturing them at different foundries. As the untrusted foundry, usually the FEOL foundry, gets only a part of the design, it is expected that they cannot reverse engineer the incomplete FEOL part to obtain the complete design. Our work shows that how an attacker can use the heuristics employed during the physical design process to reverse engineer the missing BEOL part from the FEOL part.

More details on the attack can be found at:

Y. Wang, P. Chen, J. Hu, and J. Rajendran, “The cat and mouse in split manufacturing,” ACM/IEEE Design Automation Conference, pp. 1–6, 2016.
 
## Executing the code:
 
### 1.Put .lib and .lef files in the same folder as the executable file (named “main”)
 
### 2.To run the script in the command line, use the following command:

input ./[the executable filename] [.def file path] [topmost FEOLlayer]

<b>For example:</b><br>

\>\>./main c432_45nm_routing_layer5.def 3

“topmost FEOLlayer” is the layer at which the split occurs.
 
### 3.The netlist recovered by the attacker is stored in the output file named "outnetlist."

In the output netlist file, from the left to the right:

“Component Name” indicates the name of the component, which is usually the name of the gate.

“Component Type” indicates the functionality of the component

This is followed by the connection between each pin and the corresponding wire(s). The information is separated by a colon.
 
<b>For example:</b><br>

Component Name+++Component Type+++Input Connection

U186+++AND2_X1+++|A1: N50, Primaryinput|A2: U209, ZN|

N69+++INPUT+++|PrimaryIn_in: NA|

N223+++OUTPUT+++|PrimaryOut_in: U209, ZN|

<b>Explanation:</b><br>

U186 is a two-input AND gate of type AND2_X1. Its input pin A1 is connected to the wire N50, which is a primary input. The other input pin A2 is connected to the ZN pin of gate U209.

N69 is a primary input. It is not connected to anything which is indicated as “NA.”

N223 is a primary output. It is connected to the ZN pin of U209.

## Note:

• This executable file only supports NanGate 45nm Open Cell Library:

http://www.nangate.com/?page_id=2325

You should use “NangateOpenCellLibrary.lef” and “NangateOpenCellLibrary_typical.lib.”

• The .def file should contain complete layout information (i.e. both FEOL and BEOL information). The splitting is performed internally.

• In the .def file, there should not be any floating wires.

• For now, only the following components are supported: AND, NAND, OR, NOR, INV, AOI, OAI, MUX, XOR, NXOR, BUF, DFF_X1. No other components are allowed.

Please send your comments to flwave@tamu.edu. We would highly appreciate your comments. 

