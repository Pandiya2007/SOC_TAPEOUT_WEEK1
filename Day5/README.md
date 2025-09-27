# Day 5: RTL Workshop – Optimization in Verilog Synthesis

Today, I cover optimization in Verilog synthesis, focusing on `if-else` statements, `for` loops, generate blocks, and how improper coding can lead to inferred latches. Hands-on labs are included.

---

## Contents
- [1. If-Else Statements in Verilog](#1-if-else-statements-in-verilog)  
- [2. Inferred Latches in Verilog](#2-inferred-latches-in-verilog)  
- [3. Labs for If-Else and Case Statements](#3-labs-for-if-else-and-case-statements)  
- [4. For Loops in Verilog](#4-for-loops-in-verilog)  
- [5. Generate Blocks in Verilog](#5-generate-blocks-in-verilog)  
- [6. Ripple Carry Adder (RCA)](#6-ripple-carry-adder-rca)  
- [7. Labs on Loops and Generate Blocks](#7-labs-on-loops-and-generate-blocks)  
- [Summary](#summary)  

---

## 1. If-Else Statements in Verilog

Used for conditional execution inside procedural blocks (`always`, `initial`, tasks, functions).  

```verilog
if (condition) begin
    // Executes if condition is true
end else begin
    // Executes if condition is false
end
```


## Lab 2/3: Nested If-Else
```verilog
module incomp_if2(input i0, i1, i2, i3, output reg y);
always @(*) begin
    if (i0) y <= i1;
    else if (i2) y <= i3;
end
endmodule
```

## Lab 5: Complete Case
```verilog
module comp_case(input i0, i1, i2, input [1:0] sel, output reg y);
always @(*) begin
    case(sel)
        2'b00: y = i0;
        2'b01: y = i1;
        default: y = i2;
    endcase
end
endmodule
```

## Lab 7: Incomplete Case
```verilog
module bad_case(input i0, i1, i2, i3, input [1:0] sel, output reg y);
always @(*) begin
    case(sel)
        2'b00: y = i0;
        2'b01: y = i1;
        2'b10: y = i2;
        2'b1?: y = i3; // wildcard, incomplete!
    endcase
end
endmodule
```

## Lab 8: Partial Assignments
```verilog
module partial_case_assign(input i0, i1, i2, input [1:0] sel,
                           output reg y, output reg x);
always @(*) begin
    case(sel)
        2'b00: begin y = i0; x = i2; end
        2'b01: y = i1;
        default: begin x = i1; y = i2; end
    endcase
end
endmodule
```

## Lab 9: 4-to-1 MUX Using For
```verilog
module mux_generate(input i0,i1,i2,i3, input [1:0] sel, output reg y);
wire [3:0] i_int = {i3,i2,i1,i0};
integer k;
always @(*) begin
    for (k=0;k<4;k=k+1)
        if (k == sel) y = i_int[k];
end
endmodule
```

## Lab 10: 8-to-1 Demux Using Case
```verilog
module demux_case(output o0,o1,o2,o3,o4,o5,o6,o7,
                  input [2:0] sel, input i);
reg [7:0] y_int;
assign {o7,o6,o5,o4,o3,o2,o1,o0} = y_int;
always @(*) begin
    y_int = 0;
    case(sel)
        3'b000: y_int[0] = i;
        3'b001: y_int[1] = i;
        3'b010: y_int[2] = i;
        3'b011: y_int[3] = i;
        3'b100: y_int[4] = i;
        3'b101: y_int[5] = i;
        3'b110: y_int[6] = i;
        3'b111: y_int[7] = i;
    endcase
end
endmodule
```

## Lab 11: 8-to-1 Demux Using For
```verilog
module demux_generate(output o0,o1,o2,o3,o4,o5,o6,o7,
                      input [2:0] sel, input i);
reg [7:0] y_int;
assign {o7,o6,o5,o4,o3,o2,o1,o0} = y_int;
integer k;
always @(*) begin
    y_int = 0;
    for (k=0;k<8;k=k+1)
        if (k == sel) y_int[k] = i;
end
endmodule
```

## Lab 12: 8-bit Ripple Carry Adder
```verilog
module fa(input a, b, c, output co, sum);
    assign {co, sum} = a + b + c;
endmodule

module rca(input [7:0] num1, num2, output [8:0] sum);
wire [7:0] s, c;
genvar i;
generate
    for (i=1; i<8; i=i+1)
        fa fa_i(.a(num1[i]),.b(num2[i]),.c(c[i-1]),.co(c[i]),.sum(s[i]));
endgenerate
fa fa0(.a(num1[0]),.b(num2[0]),.c(0),.co(c[0]),.sum(s[0]));
assign sum[7:0] = s;
assign sum[8] = c[7img];
endmodule
```

<img width="1024" height="1024" alt="ChatGPT Image Sep 27, 2025, 11_09_25 PM" src="https://github.com/user-attachments/assets/1623dbbe-5377-452b-82e9-4a448d894b81" />

