# 4_bit_RCA_using_function
# EXP NP: 4. 4-bit Ripple Carry Adder using Task, and 4-bit Ripple Counter using Function with Testbench
# Aim
To design and simulate a 4-bit-Ripple-counter-using-Function-and-4-bit-Ripple-Adder-using-task using Verilog HDL, and verify its functionality through a testbench in the Vivado 2023.1 environment.

# Apparatus Required
Vivado 2023.1

# Procedure

1. Launch Vivado 2023.1 Open Vivado and create a new project.
2. Design the Verilog Code Write the Verilog code for the seven-segment display, defining the logic that maps a 4-bit binary input to the corresponding segments (a to g) of the display.
3. Create the Testbench Write a testbench to simulate the seven-segment display behavior. The testbench should apply various 4-bit input values and monitor the corresponding output.
4. Create the Verilog Files Create both the design module and the testbench in the Vivado project.
5. Run Simulation Run the behavioral simulation to verify the output.
6. Observe the Waveforms Analyze the output waveforms in the simulation window, and verify that the correct segments light up for each digit.
7. Save and Document Results Capture screenshots of the waveform and save the simulation logs. These will be included in the lab report.

# Verilog Code
# 4 bit Ripple Adder using Task
// 4-bit Ripple Carry Adder using Task 
```
module ripple_adder_task ( input [3:0] A, B, input Cin, output reg [3:0] Sum, output reg Cout ); reg c; integer i;
task full_adder;
    input a, b, cin;
    output s, cout;
    begin
    ///
    end
endtask

always @(*) 
begin
    c = Cin;
    for (i = 0; i < 4; i = i + 1) begin
        full_adder(A[i], B[i], c, Sum[i], c);
    end
    Cout = c;
end
endmodule
```
Test Bench
```
module ripple_adder_task_tb;

reg [3:0] A, B;
reg Cin;

wire [3:0] Sum;
wire Cout;

ripple_adder_task uut (
    .A(A),
    .B(B),
    .Cin(Cin),
    .Sum(Sum),
    .Cout(Cout)
);

initial begin

    // Test 1: 3 + 5 = 8
    A = 4'b0011;
    B = 4'b0101;
    Cin = 1'b0;
    #10;

    // Test 2: 7 + 4 = 11
    A = 4'b0111;
    B = 4'b0100;
    Cin = 1'b0;
    #10;

    // Test 3: 9 + 6 = 15
    A = 4'b1001;
    B = 4'b0110;
    Cin = 1'b0;
    #10;

    // Test 4: 15 + 1 = 16
    A = 4'b1111;
    B = 4'b0001;
    Cin = 1'b0;
    #10;

    // Test 5: 5 + 3 + 1 = 9
    A = 4'b0101;
    B = 4'b0011;
    Cin = 1'b1;
    #10;

    $finish;
end

initial begin
    $monitor("Time=%0t | A=%b | B=%b | Cin=%b | Sum=%b | Cout=%b",
             $time, A, B, Cin, Sum, Cout);
end

endmodule
```
# Output Waveform

<img width="1705" height="898" alt="image" src="https://github.com/user-attachments/assets/6b1e0e80-6a38-4aff-9f4b-ba69d82a401d" />

# 4 bit Ripple counter using Function
// 4-bit Ripple Counter using Function 
```
module ripple_counter_func ( input clk, rst, output reg [3:0] Q );
function [3:0] count;
 ///
endfunction

always @(posedge clk or posedge rst) begin
    if (rst)
        Q <= 4'b0000;
    else
        Q <= count(Q);  // use function to increment
end
endmodule
```
Test Bench
```
module ripple_counter_func_tb;

reg clk;
reg rst;
wire [3:0] Q;

ripple_counter_func uut (
    .clk(clk),
    .rst(rst),
    .Q(Q)
);

// Clock generation
initial begin
    clk = 1'b0;
    forever #5 clk = ~clk;
end

initial begin

    // Reset
    rst = 1'b1;
    #10;

    rst = 1'b0;

    // Count
    #100;

    $finish;
end

initial begin
    $monitor("Time=%0t | RST=%b | CLK=%b | Q=%b | Decimal=%d",
             $time, rst, clk, Q, Q);
end

endmodule
```
# Output Waveform
<img width="1038" height="587" alt="image" src="https://github.com/user-attachments/assets/e1fafa90-b000-4602-97f7-27f8b27b8402" />


# Conclusion
In this experiment, a 4-bit-Ripple-counter-using-Function-and-4-bit-Ripple-Adder-using-task was successfully designed and simulated using Verilog HDL.
