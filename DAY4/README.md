# 🎯 Day 4: Gate-Level Simulation (GLS), Blocking vs. Non-Blocking, & Synthesis-Simulation Mismatch

Hey team! 🙌 Welcome to **Day 4 of the RTL Workshop**! Today we’re diving into some 🔥 essential topics:

- **🖥️ Gate-Level Simulation (GLS)**  
- **⏱️ Blocking vs Non-Blocking Assignments in Verilog**  
- **⚡ Synthesis-Simulation Mismatch**

We’ll mix **theory + practical labs** so you not only understand but can actually **see it in action**! 💡

---

## 📚 Table of Contents

1️⃣ [Gate-Level Simulation (GLS)](#1-gate-level-simulation-gls)  
2️⃣ [Synthesis-Simulation Mismatch](#2-synthesis-simulation-mismatch)  
3️⃣ [Blocking vs Non-Blocking in Verilog](#3-blocking-vs-non-blocking-in-verilog)  
 • [Blocking Statements](#31-blocking-statements)  
 • [Non-Blocking Statements](#32-non-blocking-statements)  
 • [Comparison Table](#33-comparison-table)  
4️⃣ [Labs](#4-labs)  
5️⃣ [Summary](#5-summary)  

---

## 1️⃣ Gate-Level Simulation (GLS) 🖥️

**GLS** = **Gate-Level Simulation**.  

It’s the **step where your RTL transforms into gates** (post-synthesis) and we check:

✅ Functional correctness  
⏱️ Timing behavior  
⚡ Power estimates  
🔍 Test structures (e.g., scan chains for DFT)  

### Why GLS?

- **Validate synthesis** – Make sure RTL → gates correctly  
- **Timing check** – Include real delays (from SDF files)  
- **Testability** – Scan chains, DFT structures, etc.  

### When?

- **After synthesis** → RTL has become a gate-level netlist  
- **Before layout** → Catch errors early!  

### GLS Types

- **Functional GLS** – Logic only, often zero/unit delay  
- **Timing GLS** – Realistic delays to spot timing issues  

---

## 2️⃣ Synthesis-Simulation Mismatch ⚡

When **RTL simulation ≠ Gate-Level simulation or hardware**, we call it a **mismatch**.  

Common reasons:  

❌ Non-synthesizable constructs (`#delays`, `initial` blocks)  
❌ Incomplete/ambiguous coding (`missing else`, wrong sensitivity lists)  
❌ Tool interpretation differences  

💡 **Pro tip:** Always write **synthesizable + unambiguous RTL**. Avoid surprises!  

---

## 3️⃣ Blocking vs Non-Blocking in Verilog ⏱️

Verilog gives us **two assignment styles**:

### 3.1 Blocking (`=`) ⚡

- Sequential, **executes immediately**  
- Great for **combinational logic** (`always @(*)`)  

```verilog
always @(*) y = a & b;
```
### 3.2 Non-Blocking
- **Syntax:** `<=`
- **Execution:** Scheduled, executes concurrently at the end of the time step.
- **Suitable for:** Sequential logic (e.g., `always @(posedge clk)`).
- **Example:**  
  ```verilog
  always @(posedge clk) q <= d;
  ```
  ### 3.3 Comparison Table

| **Blocking (`=`)**                        | **Non-Blocking (`<=`)**                   |
|-------------------------------------------|--------------------------------------------|
| Uses `=` operator                         | Uses `<=` operator                         |
| Sequential, immediate execution           | Concurrent, scheduled at end of timestep   |
| Updates happen instantly in code order    | Updates applied after time step            |
| For combinational logic, temp variables   | For sequential logic, registers/flip-flops |
| Infers combinational logic (gates)        | Infers sequential logic (flip-flops)       |

---
## 4. Labs

### Lab 1: Ternary Operator MUX

Verilog code for a simple 2:1 multiplexer using a ternary operator:

```verilog
iverilog /path/to/primitives.v /path/to/sky130_fd_sc_hd.v ternary_operator_mux.v testbench.v
- **Function:** `y = i1` if `sel = 1`; else `y = i0`.
---
```
<img width="1791" height="250" alt="Screenshot 2025-09-27 224026" src="https://github.com/user-attachments/assets/11bf623f-e8e9-4542-aebd-942505c0449a" />
### Lab 3: Gate-Level Simulation (GLS) of MUX

Run GLS for the synthesized MUX.  
Use this command (adjust paths as needed):

```shell
iverilog /path/to/primitives.v /path/to/sky130_fd_sc_hd.v ternary_operator_mux.v testbench.v
```
### Lab 4: Bad MUX Example (Common Pitfalls)

Verilog code with intentional issues:

```verilog
module bad_mux (input i0, input i1, input sel, output reg y);
  always @ (sel) begin
    if (sel)
      y <= i1;
    else 
      y <= i0;
  end
endmodule
```

#### Issues:
- **Incomplete sensitivity list**: Should include `i0`, `i1`, and `sel`.
- **Non-blocking assignment in combinational logic**: Should use blocking assignments (`=`).
  ### Lab 5: GLS of Bad MUX

Perform GLS on the `bad_mux`.  
Expect simulation mismatches or warnings due to above issues.
### Lab 6: Blocking Assignment Caveat

Verilog code:

```verilog
module blocking_caveat (input a, input b, input c, output reg d);
  reg x;
  always @ (*) begin
    d = x & c;
    x = a | b;
  end
endmodule
```

## 5. Summary

- **Gate-Level Simulation (GLS):** Validates netlist functionality, timing, and testability after synthesis.
- **Synthesis-Simulation Mismatch:** Avoid by using synthesizable, unambiguous RTL code.
- **Blocking vs. Non-Blocking:** Use blocking (`=`) for combinational, non-blocking (`<=`) for sequential logic.
- **Labs:** Reinforce key concepts and highlight common RTL pitfalls.

---

