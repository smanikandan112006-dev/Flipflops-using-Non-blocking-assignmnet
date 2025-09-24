# EXPERIMENT 3B: Simulation of All Flip-Flops using Non Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **Non blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **Non blocking assignment (`<=`)** inside the `always` block.  
Non Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

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

### SR Flip-Flop (Non Blocking)
```verilog
`timescale 1ns / 1ps


module SRflipflop(S,R,clk,reset,q);
input S,R,clk,reset;
output reg q;
always @ (posedge clk)
begin
if (reset==1)
q<=0;
else 
begin 
case({S,R})
2'b00:q<=q;
2'b01:q<=1'b0;
2'b10:q<=1'b1;
2'b11:q<=1'bx;
endcase
end
end
endmodule
```
### SR Flip-Flop Test bench 
```verilog
module tb_srff;
  reg S, R, clk, reset;
  wire Q;

  SRflipflop UUT (S, R, clk, reset, Q);

  always #5 clk = ~clk;

  initial begin
    clk = 0; S = 0; R = 0; reset = 1;

    #10 reset = 0;
    #10 S = 1; R = 0;
    #10 S = 0; R = 0;
    #10 S = 0; R = 1;
    #10 S = 1; R = 1;
    #10 S = 0; R = 0;

    #20 $finish;
  end
endmodule




```
#### SIMULATION OUTPUT

<img width="457" height="286" alt="image" src="https://github.com/user-attachments/assets/1cdf3465-5916-4488-8bb5-b2880193d156" />

---

### JK Flip-Flop (Non Blocking)
```verilog
`timescale 1ns / 1ps

module JKflipflop(J, K, clk, reset, q);
input J, K, clk, reset;
output reg q;
always @ (posedge clk) begin
if (reset == 1)
q<=0;   
else begin
case ({J, K})
2'b00: q <= q;     
2'b01: q <= 1'b0;  
2'b10: q <= 1'b1;  
2'b11: q <= ~q;    
endcase
end
end
endmodule




endmodule
```
### JK Flip-Flop Test bench 
```verilog
module tb_jkff;
reg J, K, clk, reset;
wire Q;
JKflipflop uut (J, K, clk, reset, Q);
always #5 clk = ~clk;
initial begin
clk = 0; J = 0; K = 0; reset = 1;

#10 reset = 0;
#10 J = 1; K = 0;   
#10 J = 0; K = 1;   
#10 J = 1; K = 1;   
#10 J = 0; K = 0;   
#10 J = 1; K = 1;   
#20 $finish;
end
endmodule

```
#### SIMULATION OUTPUT

<img width="457" height="286" alt="image" src="https://github.com/user-attachments/assets/2b733465-810d-4e98-b94c-355e4b98f6fd" />

---
### D Flip-Flop (Non Blocking)
```verilog
`timescale 1ns / 1ps

module Dflipflop(D, clk, reset, Q);
input D, clk, reset;
output reg Q;

always @ (posedge clk) begin
if (reset == 1)
Q <= 0;        
else
Q <= D;        
end
endmodule
```
### D Flip-Flop Test bench 
```verilog

module tb_dff;
reg D, clk, reset;
wire Q;
Dflipflop UUT (D, clk, reset, Q);
  always #5 clk = ~clk;

initial begin
clk = 0; D = 0; reset = 1;
#10 reset = 0;
#10 D = 1;   
#10 D = 0;   
#10 D = 1;   
#10 D = 1;   
#10 D = 0;   
#10 D = 1;   

#20 $finish;
end
endmodule



```

#### SIMULATION OUTPUT

<img width="458" height="287" alt="image" src="https://github.com/user-attachments/assets/980aa5fc-5603-4e95-9481-5c908a1f5337" />

---
### T Flip-Flop (Non Blocking)
```verilog
`timescale 1ns / 1ps

module Tflipflop(T, clk, reset, Q);
  input T, clk, reset;
  output reg Q;

  always @ (posedge clk) begin
    if (reset == 1)
      Q <= 0;          
    else if (T == 1)
      Q <= ~Q;         
    else
      Q <= Q;          
  end
endmodule


```
### T Flip-Flop Test bench 
```verilog
module tb_tff;
  reg T, clk, reset;
  wire Q;

  
  Tflipflop UUT (T, clk, reset, Q);

  
  always #5 clk = ~clk;

  initial begin
    
    clk = 0; T = 0; reset = 1;

   
    #10 reset = 0;

    
    #10 T = 1;   
    #20 T = 0;   
    #20 T = 1;   
    #20 T = 0;  

    #20 $finish;
  end
endmodule




```

#### SIMULATION OUTPUT

<img width="459" height="287" alt="image" src="https://github.com/user-attachments/assets/98d819ec-b529-4e95-912f-0eb99b3f5a0a" />


---

### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using Non blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
