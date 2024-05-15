# VLSI-LAB-EXP-4
# SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

# AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023.1.

# APPARATUS REQUIRED:

Vivado 2023.1

**LOGIC DIAGRAM**

# SR FLIPFLOP
![301740946-77fb7f38-5649-4778-a987-8468df9ea3c3](https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/20f4274e-5313-4992-b5a8-f0539e0927c7)



# JK FLIPFLOP
![301743103-1510e030-4ddc-42b1-88ce-d00f6f0dc7e6](https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/870bf235-f1b5-446b-9cfc-5ae92a0deb73)



# T FLIPFLOP
![301743290-7a020379-efb1-4104-85ee-439d660baa08](https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/8f782dbe-0bd4-4c91-a16d-cfd933ff5bb2)




# D FLIPFLOP
![301743389-dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0](https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/e16a5f80-f144-44fa-89db-f7b512cd76de)


# COUNTER

![301743514-a1fc5f68-aafb-49a1-93d2-779529f525fa](https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/24317f63-09a9-445e-904d-e550c120d5b7)


# PROCEDURE:
1.Open Vivado: Launch Xilinx Vivado software on your computer.
2.Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".
3.Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.
4.Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.
5.Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).
6.Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.
7.Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.
8.Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.
9.View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.

# D-FLIP FLOP
VERILOG CODE
~~~
module Dflipflop(D,clk,reset,Q);
input D;
input clk;
input reset;
output reg Q;
always @(posedge clk)
begin
 if(reset==1'b1)
  Q <= 1'b0;
 else
  Q <= D;
end
endmodule
~~~

# OUTPUT:
<img width="962" alt="329915856-03e5b43e-8fd1-42db-bec9-d8e1cd6342b0" src="https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/3e155815-2ba4-4170-8cbf-fee041decb74">
<img width="962" alt="329915890-3b92b980-ac92-4606-a838-c6d9648e3a01" src="https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/6c35a4b3-168a-4db1-aea6-a22b4dfba96f">


# JK FLIP FLOP

VERILOG CODE:
~~~
module JK_flipflop (q, q_bar, j,k, clk,reset);
input j,k,clk, reset;
output reg q;
output q_bar;
always@(posedge clk)
begin
  if(!reset)        
    q <= 0;
  else 
  begin
      case({j,k})
        2'b00: q <= q;    // No change
        2'b01: q <= 1'b0; // reset
        2'b10: q <= 1'b1; // set
        2'b11: q <= ~q; // Toggle
      endcase
  end
end
assign q_bar = ~q;
endmodule
~~~

# OUTPUT:
<img width="962" alt="329915958-4a094ca4-dfb9-47e5-8a78-b95b280128cf" src="https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/264c6631-a2c7-49ec-936f-584b8a50e7c2">
<img width="962" alt="329916044-8e770e54-6496-4f60-85cb-b508304bc995" src="https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/1998b582-503d-4cfc-852f-4a26e291014a">


# MOD-10 COUNTER

VERILOG CODE:
~~~
module mod10(clk,rst,out);
input clk,rst;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1 | out==4'b1001)
out=4'b0000;
else
out=out+1;
end
endmodule
~~~

# OUTPUT:
<img width="962" alt="329916097-35aedae2-4db5-4e7d-8adf-6c4fd4293013" src="https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/ccdd6534-7334-4125-b55c-b3af9414073f">
<img width="962" alt="329916128-01a592b8-068c-4dca-be79-f060cf02930f" src="https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/2a424d8d-a5a4-4098-8fef-f4ea541e1d9c">




# RIPPLE CARRY COUNTER

VERILOG CODE:
~~~
module tff(q,clk,rst);
input clk,rst;
output q;
wire d;
dff df1(q,d,clk,rst);
not n1(d,q);
endmodule
module dff(q,d,clk,rst);
input d,clk,rst;
output q;
reg q;
always @(posedge clk or posedge rst)
begin
if (rst)
q=1'b0;
else 
q=d;
end
endmodule
module ripplecounter(clk,rst,q);
input clk,rst;
output [3:0]q;
tff tf0(q[0],clk,rst);
tff tf1(q[1],q[0],rst);
tff tf2(q[2],q[1],rst);
tff tf3(q[3],q[2],rst);
endmodule
~~~

# OUTPUT:
<img width="962" alt="329916188-b3729306-b93d-4b9b-8f30-31e23103d84e" src="https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/5b00e0e9-a392-489f-8aa8-638c880a7481">
<img width="962" alt="329916212-af913a78-3179-4fbb-b0e6-ee33c1efb1cf" src="https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/804ef459-b045-4217-a241-e51e4c6ec751">


# SR FLIP FLOP

VERILOG CODE:
~~~
module sr_flipflop(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=1'bX;
endcase
end
end
endmodule
~~~

# OUTPUT:
<img width="962" alt="329916278-bdee999f-58b1-4a98-95a8-11411516bdc3" src="https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/3c50f36c-c3e4-48d7-a1de-507ee1cb7bd8">
<img width="962" alt="329916308-26a92567-0cf6-41da-ac9d-d5afc43d865d" src="https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/92cacbb7-399d-46f5-95c7-a3e3c102f78a">


# T FLIP FLOP

VERILOG CODE:
~~~
module T_flipflop(clk,rst,t,q);
input clk,rst,t;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else if (t==0)
q=q;
else
q=~q;
end
endmodule
~~~

# OUTPUT:
<img width="962" alt="329916401-64d9a351-3be8-4bb5-9b09-40ec166f94be" src="https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/80eab3b9-7761-4c55-adcd-c09e9ad77439">
<img width="962" alt="329916437-6540708a-a079-4138-a05d-a326b34277fa" src="https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/b3b0ed53-b2da-48d2-b24f-97ae538a2c4a">


# UP-DOWN COUNTER

VERILOG CODE:
~~~
module updown_counter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
~~~

# OUTPUT:

<img width="617" alt="329916515-530d78ab-9c07-4497-b308-fea125c000c3" src="https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/5f31eb93-2a76-477d-875b-18dca4ac3074">
<img width="962" alt="329916546-9b5a2a72-aaf6-451b-ac4d-d2774f326aaf" src="https://github.com/magesh0123/VLSI-LAB-EXP-4/assets/162102402/1195c751-f289-49c3-9d0f-02ce329dfbe1">



RESULT:
Hence The simulation and synthesis of SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023 is done and output verified successfully.
