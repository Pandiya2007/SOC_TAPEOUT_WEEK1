# Day 5: Optimization in Synthesis

Welcome to Day 5 of the RTL workshop! Today, we will cover optimization in Verilog synthesis, focusing on `if-else` statements, `for` loops, generate blocks, and explore how improper coding can lead to inferred latches. Labs are included for hands-on experience.

---
# 📘 Contents  

- [1️⃣ If-Else Statements in Verilog](#1-if-else-statements-in-verilog)  
- [2️⃣ Inferred Latches in Verilog](#2-inferred-latches-in-verilog)  
- [3️⃣ Labs for If-Else and Case Statements](#3-labs-for-if-else-and-case-statements)  
  - [🧪 Lab 1: Incomplete If Statement](#lab-1-incomplete-if-statement)  
  - [🔍 Lab 2: Synthesis Result of Lab 1](#lab-2-synthesis-result-of-lab-1)  
  - [🧩 Lab 3: Nested If-Else](#lab-3-nested-if-else)  
  - [📊 Lab 4: Synthesis Result of Lab 3](#lab-4-synthesis-result-of-lab-3)  
  - [✅ Lab 5: Complete Case Statement](#lab-5-complete-case-statement)  
  - [⚡ Lab 6: Synthesis Result of Lab 5](#lab-6-synthesis-result-of-lab-5)  
  - [⚠️ Lab 7: Incomplete Case Handling](#lab-7-incomplete-case-handling)  
  - [✂️ Lab 8: Partial Assignments in Case](#lab-8-partial-assignments-in-case)  

- [4️⃣ For Loops in Verilog](#4-for-loops-in-verilog)  
- [5️⃣ Generate Blocks in Verilog](#5-generate-blocks-in-verilog)  
- [6️⃣ What is an RCA (Ripple Carry Adder)? 🤔](#6-what-is-an-rca-ripple-carry-adder)  
- [7️⃣ Labs on Loops and Generate Blocks](#7-labs-on-loops-and-generate-blocks)  
  - [🎛️ Lab 9: 4-to-1 MUX Using For Loop](#lab-9-4-to-1-mux-using-for-loop)  
  - [🎚️ Lab 10: 8-to-1 Demux Using Case](#lab-10-8-to-1-demux-using-case)  
  - [🔄 Lab 11: 8-to-1 Demux Using For Loop](#lab-11-8-to-1-demux-using-for-loop)  
  - [➕ Lab 12: 8-bit Ripple Carry Adder with Generate Block](#lab-12-8-bit-ripple-carry-adder-with-generate-block)  

- [✨ Summary](#summary)  
## 1. If-Else Statements in Verilog

**If-else statements** are used for conditional execution in behavioral modeling, typically within procedural blocks (`always`, `initial`, tasks, or functions).

### Syntax

```verilog
if (condition) begin
    // Code block executed if condition is true
end else begin
    // Code block executed if condition is false
end
```


---
