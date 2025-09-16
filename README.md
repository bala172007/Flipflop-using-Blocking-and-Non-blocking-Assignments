# Flipflop-using-Blocking-and-Non-blocking-Assignments
Exp 3 -Write and simulate D, SR, JK, T Flipflops using Blocking and Non blocking Assignments
   Aim: To design and simulate D, SR, JK, T Flipflops using Blocking and Non blocking Assignments in Verilog HDL and verify its functionality through a testbench using the Vivado 2023.1 simulation environment.
   
  Apparatus Required:
  Vivado 2023.1
Procedure:

Launch Vivado Open Vivado 2023.1 by double-clicking the Vivado icon or searching for it in the Start menu. 
Create a New Project Click on "Create Project" from the Vivado Quick Start window. In the New Project Wizard: Project Name: Enter a name for the project (e.g., Mux4_to_1). 
Project Location: Select the folder where the project will be saved. Click Next. 
Project Type: Select RTL Project, then click Next. Add Sources: Click on "Add Files" to add the Verilog files (e.g., mux4_to_1_gate.v, mux4_to_1_dataflow.v, etc.). 
Make sure to check the box "Copy sources into project" to avoid any external file dependencies. 
Click Next.
Add Constraints: Skip this step by clicking Next (since no constraints are needed for simulation). 
Default Part Selection: You can choose a part based on the FPGA board you are using (if any). 
If no board is used, you can choose any part, for example, xc7a35ticsg324-1L (Artix-7). 
Click Next, then Finish.
Add Verilog Source Files In the "Sources" window, right-click on "Design Sources" and select Add Sources if you didn't add all files earlier.
Add the Verilog files and the testbench. 
Check Syntax Expand the "Flow Navigator" on the left side of the Vivado interface. 
Simulate the Design In the Flow Navigator, under "Simulation", click on "Run Simulation" → "Run Behavioral Simulation". 
Vivado will open the Simulations Window, and the waveform window will show the signals defined in the testbench. 
View and Analyze Simulation Results Adjust Simulation Time To run a longer simulation or adjust timing, go to the Simulation Settings by clicking "Simulation" → "Simulation Settings". Under "Simulation", modify the Run Time (e.g., set to 1000ns).
Generate Simulation Report Once the simulation is complete, you can generate a simulation report by right-clicking on the simulation results window and selecting "Export Simulation Results".
Save the report for reference in your lab records. Save and Document Results Save your project by clicking File → Save Project.
Take screenshots of the waveform window and include them in your lab report to document your results. 
You can include the timing diagram from the simulation window showing the correct functionality of the Seven Segment across different select inputs and data inputs. 
Close the Simulation Once done, by going to Simulation → "Close Simulation

Input/Output Signal Diagram:

***D FF***

***SR FF***

***JK FF***

***T FF***


RTL Code:
***D Flip flop***
```
module dff ( clk, rst,d, q);
input clk,rst,d;
output reg q;
    always @(posedge clk) begin
        if (rst)   
            q <= 1'b0;
        else
            q <= d;  
    end
endmodule
```
TestBench:
***D Flip flop***
```
module dff_tb;
    reg clk_t, rst_t, d_t;
    wire q_t;
    dff dut (.clk(clk_t),.rst(rst_t),.d(d_t),.q(q_t) );
    initial begin
        clk_t = 1'b0;
        rst_t = 1'b1;  
        d_t   = 1'b0;
        #100 rst_t = 1'b0; 
        #100 d_t = 1'b1;
        #100 d_t = 1'b0;
        #100 d_t = 1'b1;
end
     always #10 clk_t = ~clk_t;
endmodule
```
Output waveform:
***D Flip flop***
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/6b64f624-5877-4ed9-b0c0-2ee916b3a40a" />

Conclusion:


