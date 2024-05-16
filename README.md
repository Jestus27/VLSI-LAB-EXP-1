# VLSI-LAB-EXPERIMENTS
**AIM:**

 To simulate and synthesis Logic Gates,Adders and Subtractor using Xilinx ISE.

**APPARATUS REQUIRED:**

 Vivado 2023.1

**PROCEDURE:**

STEP:1 Start the Xilinx navigator, Select and Name the New project. 

STEP:2 Select the device family, device, package and speed. 

STEP:3 Select new source in the New Project and select Verilog Module as the Source type. 

STEP:4 Type the File Name and Click Next and then finish button. Type the code and save it. 

STEP:5 Select the Behavioral Simulation in the Source Window and click the check syntax. 

STEP:6 Click the simulation to simulate the program and give the inputs and verify the outputs as per the truth table. 

STEP:7 Select the Implementation in the Sources Window and select the required file in the Processes Window. 

STEP:8 Select Check Syntax from the Synthesize XST Process. Double Click in the Floorplan Area/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 

STEP:9 In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu. 

STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here. 

STEP:11 Load the Bit file into the SPARTAN 6 FPGA STEP:11 On the board, by giving required input, the LEDs starts to glow light, indicating the output.

Logic Diagram :


Logic Gates:
![301405876-ee17970c-3ac9-4603-881b-88e2825f41a4](https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/6c0fefc1-5e35-4e2a-a7e6-a43307c59025)



Half Adder:

![301406331-0e1ecb96-0c25-4556-832b-aeeedfdfe7b9](https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/d2824b19-c614-4450-8e48-4ca53009ba06)


Full adder:

![301406527-9bb3964c-438f-469d-a3de-c1cca6f323fb](https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/356a5336-2ab6-47d4-82d9-e8c33a3e6a8d)



Half Subtractor:

![301406051-731470b7-eb4e-49f8-8bb7-2994052a7184](https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/87d90f41-33f6-46dd-818e-9dd509484811)



Full Subtractor:

![301406088-d66f874b-c1f2-44b3-a035-7149b56430c1](https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/3c7cfc11-e688-43f8-a535-baf265887eaa)



8 Bit Ripple Carry Adder

![301406117-7385a408-40a5-4203-8050-b72818622d79](https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/55e24d85-0a84-41dc-8696-fca8777a0b81)




VERILOG CODE:

# Full Adder:
```
module fulladder (sum, cout, a,b,c);
input a,b,c;
output sum, cout;
wire w1,w2,w3,w4,w5;
xor x1(w1,a,b);
xor x2(sum,w1,c);
and al(w2,a,b);
and a2(w3,b,c);
and a3(w4,a,c);
or o1(w5,w2,w3); or o2(cout,w5,w4);
endmodule
```
# Full Subractor:
```
module full_subtractor(a, b, c,D, Bout);
input a, b, c;
output D, Bout;
assign D = a^b^c;
assign Bout = (~a & b) | (~(a^ b) & c);
endmodule
```
# Half Adder:
```
module half_adder(a,b,sum,carry);
input a,b;
output sum,carry;
or(sum,a,b);
and(carry,a,b);
endmodule
```
# Half Subractor:
```
module half_subtractor(D,Bo,A,B);
input A,B;
output D,Bo;
assign D=A^B;
assign Bo=(~A)&B;
endmodule
```
# Logic Gates:
```
module logicgates(a,b,andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate);
input a,b;
output andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate;
and(andgate,a,b);
or(orgate,a,b);
xor(xorgate,a,b);
nand(nandgate,a,b);  
nor(norgate,a,b);
xnor(xnorgate,a,b);
not(notgate,a);
endmodule
```
# Ripple Carry Adder 4Bit:
```
module rippe_adder(S, Cout, X, Y,Cin);
 input [3:0] X, Y;// Two 4-bit inputs
 input Cin;
 output [3:0] S;
 output Cout;
 wire w1, w2, w3;fulladder u1(S[0], w1,X[0], Y[0], Cin);
 fulladder u2(S[1], w2,X[1], Y[1], w1);
 fulladder u3(S[2], w3,X[2], Y[2], w2);
 fulladder u4(S[3], Cout,X[3], Y[3], w3);
endmodule
module fulladder(S, Co, X, Y, Ci);
  input X, Y, Ci;
  output S, Co;  
  wire w1,w2,w3;  
  xor G1(w1, X, Y); 
  xor G2(S, w1, Ci);
  and G3(w2, w1, Ci);
  and G4(w3, X, Y);
  or G5(Co, w2, w3);
endmodule
```
# Ripple Carry Adder 8bit
```
module fulladder(a,b,c,sum,carry);
input a,b,c;
output sum,carry;
wire w1,w2,w3;
xor(w1,a,b);
xor(sum,w1,c);
and(w2,w1,c);
and(w3,a,b);
or(carry,w2,w3);
endmodule

module rca_8bit(a,b,cin,s,cout);
input [7:0]a,b;
input cin;
output [7:0]s;
output cout;
wire [7:1]w;
fulladder f1(a[0], b[0], cin, s[0], w[1]);
fulladder f2(a[1], b[1], w[1], s[1], w[2]);
fulladder f3(a[2], b[2], w[2], s[2], w[3]);
fulladder f4(a[3], b[3], w[3], s[3], w[4]);
fulladder f5(a[4], b[4], w[4], s[4], w[5]);
fulladder f6(a[5], b[5], w[5], s[5], w[6]);
fulladder f7(a[6], b[6], w[6], s[6], w[7]);
fulladder f8(a[7], b[7], w[7], s[7], cout);
endmodule
```

OUTPUT:

# Full Adder:

![324402623-22107c6d-d04c-4bef-aec0-eeed5a79c44a](https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/9da87612-f76f-4a55-87b7-e64c072769a3)

<img width="632" alt="324402675-492ae14a-c23e-409a-8182-969b5b2b4c2b" src="https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/dd32baf4-0a88-482a-8eba-eb74ee91efb0">

# Full Subractor:

![324402821-085e478a-dbd1-4afc-92c8-1107327e6ada](https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/9698c902-c33c-4c23-9cbd-b4e399c2a447)

<img width="490" alt="324402886-4cf9ad2c-06c7-4fba-875a-215221954321" src="https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/200430eb-dbdd-4eda-91f5-883510da1b13">

# Half Adder:

![324402988-2e11b29e-a43e-41bd-91dd-11ddfa0049bd](https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/3cbf9482-03a9-4b53-a03a-f49f7cafe3ef)

![324403108-9d50e021-22e8-48e9-820e-e1062eac93ff](https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/2892f94d-0821-4ecd-8566-50061df0bd6d)


# Half Subractor:

![324403213-6a4ca03b-935a-4def-be95-cb9cae73a07b](https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/3c3fcd36-7ac7-425e-abc3-1230d561b14f)

<img width="488" alt="324403263-381744ae-7a6c-4824-a167-f70f69d932bb" src="https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/447e0d86-694c-47e2-b866-92984326abe2">


# Logic Gates:

![324403363-400d2234-6df2-42bf-ae50-7a191c1b52a7](https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/8385c1de-dc92-4170-be5c-af45ab89229f)

<img width="556" alt="324403417-e2f52b34-b8bd-441f-8d48-b024cb366f5e" src="https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/02755fc3-9927-4ad6-b151-ca97679df7e7">

# Ripple Carry Adder 4bit:

![324403510-43fe924e-9a74-4359-a83e-ea0956df124b](https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/8e4ad7f6-481a-4da9-a74b-920fb131775e)

<img width="632" alt="324403576-4ab2d8b9-2f06-43be-a42e-945359c4793b" src="https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/904f020e-63c9-451c-813e-84d7d64f3f20">

# Ripple Carry Adder 8bit:

![324403643-8dd8b2d4-057f-4a2a-9496-2775480038d5](https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/f6b997df-af3c-488a-b7b9-57e91deb6d96)

<img width="631" alt="324403695-da885a29-0c7e-4c71-a8e1-1c9dbd3e555e" src="https://github.com/Jestus27/VLSI-LAB-EXP-1/assets/167751233/0827ac48-940f-4c8f-982d-75be689e746a">

RESULT:Thus the simulation and synthesis Logic Gates,Adders and Subtractor using VIVADO 2023.2 has been verified.

