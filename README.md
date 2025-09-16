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

***Input/Output Signal Diagram:***

***D Flip Flop***

<img width="495" height="246" alt="image" src="https://github.com/user-attachments/assets/a870e780-d46f-48ca-8321-d73a10e89acd" />

***SR Flip Flop***

<img width="485" height="290" alt="image" src="https://github.com/user-attachments/assets/fe9aa70a-2a4a-4b7b-b171-79ad0689dfdd" />

***JK Flip Flop***

<img width="453" height="283" alt="image" src="https://github.com/user-attachments/assets/dec9c5d2-cfa5-41ec-a92c-355cb944dcab" />

***T Flip Flop***

<img width="483" height="270" alt="image" src="https://github.com/user-attachments/assets/f4fa2c9a-db72-4b47-928f-8690e39a65d9" />


***RTL Code:***

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

***SR Flip Flop***
```
module sr_ff (input clk,input S,input R,output reg Q);
always @(posedge clk)
 begin
    case ({S,R})
      2'b00: Q <= Q;    
      2'b01: Q <= 0;    
      2'b10: Q <= 1;    
      2'b11: Q <= 1'bx; 
 endcase
 end
endmodule
```

***JK Flip Flop***
```
module jk_ff(input clk,J,K, output reg Q);
always @(posedge clk) begin
case({J,K})
2'b00: Q<=Q;
2'b01: Q<=0;
2'b10: Q<=1;
2'b11: Q<=~Q;
endcase
end
endmodule
```

***T Flip Flop***
```
module t_ff(clk,rst,Tout,T);
    input clk,rst,T;
    output reg Tout;
    always@ (posedge clk)
     begin
     if(rst)
        Tout = 1'b0;
     else if(T)
        Tout = ~Tout;
     else
        Tout = Tout;
     end
endmodule
```

***TestBench:***

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
***SR Flip Flop***
```
module sr_ff_tb;
  reg clk, S, R;
  wire Q;
  sr_ff uut (.clk(clk),.S(S),.R(R),.Q(Q));
  initial begin
   clk = 0;
  forever #10 clk = ~clk; 
  end
  initial begin
    S = 0; R = 0;
    #100 S = 1; R = 0;   
    #100 S = 0; R = 0;   
    #100 S = 0; R = 1;   
    #100 S = 1; R = 1;  
    #100 S = 0; R = 0;
 end
endmodule
```

***JK Flip Flop***
```
module tb_jk_ff;
  reg clk;
  reg J, K;
  wire Q;
  jk_ff uut (.clk(clk),.J(J),.K(K),.Q(Q));
initial begin
clk=0;
forever #20 clk=~clk;
end
initial begin
 J = 0; K = 0;
    #100 J=0; K=0;  
    #100 J=0; K=1; 
    #100 J=1; K=0;  
    #100 J=1; K=1;  
    #100 J=0; K=1; 
    #100 J=1; K=0;  
    #100 J=1; K=1;  
end
endmodule
```

***T Flip Flop***
```
module t_ff_tb;
  reg clk, rst, T;
  wire Tout;
  t_ff uut (.clk(clk),.rst(rst),.T(T),.Tout(Tout));
  initial begin
    clk = 0;
    forever #10 clk = ~clk;  
  end
  initial begin
    
    rst = 1; T = 0;
    #20 rst = 0;    
    #20 T = 1;      
    #20 T = 0;      
    #20 T = 1;      
    #20 T = 1;      
    #20 T = 0;
  end

endmodule
```

***Output waveform:***

***D Flip flop***

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/6b64f624-5877-4ed9-b0c0-2ee916b3a40a" />

***SR Flip Flop***

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/c047331e-2b26-45ad-85cb-ee45880ead7f" />

***JK Flip Flop***

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/fa01ab1e-6a8a-43e5-a271-10f3ae4114a4" />

***T Flip Flop***

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/b11eb968-0057-4f08-a393-7603c69bb030" />

***Conclusion:***

In this experiment, various flip-flops (JK, T, D, and SR) were successfully designed and simulated using Verilog HDL. Different modeling styles were applied to implement each flip-flop. The simulation results confirmed the correct functionality of all flip-flops, with each design accurately responding to the applied inputs and clock signals. The outputs matched the expected behavior for every type of flip-flop, thereby verifying the correctness of the Verilog implementations.
