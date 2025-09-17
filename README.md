# EXPERIMENT 3: Simulation of All Flip-Flops using Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **blocking assignment (`=`)** inside the `always` block.  
Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Blocking)
```verilog
module SR_FF(S,R,clk,res,Q);
input S,R,clk,res;
output reg Q;
always @(posedge clk)
begin
if (res == 1)
    Q=0;
else
    begin
    case({S,R})
        2'b00:Q=Q;
        2'b01:Q=1'b1;
        2'b10:Q=1'b0;
        2'b11:Q=1'bx;
    endcase
    end
end        
endmodule
```
### SR Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module SR_FF_tb;
reg S,R,clk,res;
wire Q;
SR_FF uut(S,R,clk,res,Q);
always #5clk = ~clk;
initial begin
clk =0; S =1'b0; R =1'b0; res =1;
#10 res = 0;
#10 S=1'b1; R=1'b0;
#10 S=1'b0; R=1'b1;
#10 S=1'b1; R=1'b1;
#10 S=1'b0; R=1'b0;
#20
$finish;
end
endmodule

```
#### SIMULATION OUTPUT

<img width="692" height="432" alt="image" src="https://github.com/user-attachments/assets/db7c3b72-7354-4a5d-9644-fb9bd711211f" />

---

### JK Flip-Flop (Blocking)
```verilog
module JK_FF(J,K,clk,res,Q);
input J,K,clk,res;
output reg Q;
always @(posedge clk)
begin
if (res == 1)
    Q=0;
else
    begin
    case({J,K})
        2'b00:Q=Q;
        2'b01:Q=1'b1;
        2'b10:Q=1'b0;
        2'b11:Q=~Q;
    endcase
    end
end        
endmodule
```
### JK Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module JK_FF_tb;
reg J,K,clk,res;
wire Q;
JK_FF uut(J,K,clk,res,Q);
always #5clk = ~clk;
initial begin
clk =0; J =1'b0; K =1'b0; res =1;
#10 res = 0;
#10 J=1'b1; K=1'b0;
#10 J=1'b0; K=1'b1;
#10 J=1'b1; K=1'b1;
#10 J=1'b0; K=1'b0;
#20
$finish;
end
endmodule

```
#### SIMULATION OUTPUT

<img width="692" height="432" alt="image" src="https://github.com/user-attachments/assets/e1fc82d9-0c88-4481-baa1-5e9d7a595a6c" />

---
### D Flip-Flop (Blocking)
```verilog
module D_FF(D,Q, clk, res);
input D, clk, res;
output reg Q;

always @ (posedge clk) 
begin
    if (res == 1)
        Q = 0;        
    else
        Q = D;        
end
endmodule
```
### D Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module D_FF_tb;
reg D, clk, res;
wire Q;
D_FF UUT (D,Q, clk, res);
  always #5 clk = ~clk;

initial begin
clk = 0; D = 0; res = 1;
#10 res = 0;
#10 D = 1;   
#10 D = 0;   
#10 D = 0;   
#10 D = 1;   
#10 D = 1;   
#10 D = 1;   
#20 
$finish;
end
endmodule

```

#### SIMULATION OUTPUT

<img width="692" height="432" alt="image" src="https://github.com/user-attachments/assets/6e79bf83-d156-437e-bad2-af01e0f366f8" />

---
### T Flip-Flop (Blocking)
```verilog
module T_FF(T,Q,clk,res);
input T,clk,res;
output reg Q;
always @(posedge clk)
begin
if (res == 1)
    Q = 0;
else if (T==0)
    Q=Q;
else 
    Q=~Q;
end
endmodule
```
### T Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module T_FF_tb;
reg clk,res,T;
wire Q;
T_FF uut(T,Q,clk,res);
always #5 clk = ~clk;
initial
begin
clk=0 ; T=0; res=1;
#10 res=0;
#10 T = 1;
#20 T = 1;
#20 T = 0;
#20 
$finish;

end
endmodule

```

#### SIMULATION OUTPUT

<img width="692" height="432" alt="image" src="https://github.com/user-attachments/assets/87f17534-20bb-4ac7-886b-f8af77274869" />


---

### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
