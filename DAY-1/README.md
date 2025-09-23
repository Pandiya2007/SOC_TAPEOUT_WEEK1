

# **Day 1: Kickstart Your RTL Journey – Verilog, Simulation & Synthesis**

Welcome to **Day 1** of the RTL Workshop! 🎉  
Today marks the beginning of an exciting journey into **digital design**, where I’ll learn how to **describe, test, and synthesize digital circuits** using Verilog. We’ll explore open-source simulation with **Icarus Verilog (iverilog)** and get a sneak peek at **Yosys**, the tool that transforms your Verilog code into real hardware blueprints. Throughout this workshop, you’ll not just read theory—you’ll **write code, run simulations, analyze circuits, and even perform logic synthesis**, giving you a solid, hands-on foundation in RTL design. By the end of today, you’ll feel confident taking a simple Verilog design and seeing it come alive, from simulation waveforms to gate-level netlists! 🚀  

---

## **Table of Contents**

1. [What is a Simulator, Design, and Testbench?](#1-what-is-a-simulator-design-and-testbench)  
2. [Getting Started with Icarus Verilog](#2-getting-started-with-iverilog)  
3. [Lab: Simulating a 2-to-1 Multiplexer](#3-lab-simulating-a-2-to-1-multiplexer)  
4. [Breaking Down the Multiplexer Code](#4-breaking-down-the-multiplexer-code)  
5. [Introduction to Yosys & Gate Libraries](#5-introduction-to-yosys--gate-libraries)  
6. [Lab: Synthesizing Your First Design](#6-lab-synthesizing-your-first-design)  
7. [Summary & Key Takeaways](#7-summary--key-takeaways)  

---

## 1. What is a Simulator, Design, and Testbench?

### **Simulator**  
Think of a **simulator** as your circuit’s “playground.” It allows you to **test your design in a virtual environment**, apply inputs, and observe outputs—without touching a single physical wire. This is your first step to **catching bugs early** and understanding how your circuit behaves.

### **Design**  
The **design** is the heart of your digital circuit. This is your **Verilog code**, describing how logic gates and flip-flops work together to perform a task.

### **Testbench**  
A **testbench** is like your circuit’s personal trainer. It **applies various inputs** to your design and checks if the outputs behave as expected. Without a testbench, you’re basically flying blind!

<div align="center">
  <img src="https://github.com/user-attachments/assets/93927b96-df80-4da5-b801-284fc2cc6757" alt="Design & Testbench Overview" width="70%">
</div>

---

## 2. Getting Started with Icarus Verilog

**Icarus Verilog (iverilog)** is an open-source simulator that lets you **run and verify your Verilog designs**.  

Here’s how the simulation flow works:

<div align="center">
  <img src="https://github.com/user-attachments/assets/3ca190fb-cfa4-4abb-b9e1-0151b3c4bdba" alt="iverilog Simulation Flow" width="70%">
</div>

- You provide **both your design and testbench** to iverilog.  
- The simulator executes your code and produces a **`.vcd` waveform file**.  
- You can then open this file in **GTKWave** to visually inspect your signals and verify functionality.  

Simulation is **fun and satisfying**—it’s like watching your digital circuit “come alive” on screen! 🌟  

---

## 3. Lab: Simulating a 2-to-1 Multiplexer

Let’s get our hands dirty with a **simple 2-to-1 multiplexer**!  

### **Step 1: Clone the Workshop Repository**
```bash
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
```


 ###  Step 2: Install Required Tools

```shell
sudo apt install iverilog
sudo apt install gtkwave
```

###  Step 3: Simulate the Design

Compile the design and testbench:

```shell
iverilog good_mux.v tb_good_mux.v
```
Run the simulation:

```shell
./a.out
```

View the waveform:

```shell
gtkwave tb_good_mux.vcd
```

<div align="center">
  <img width="1890" height="897" alt="Screenshot 2025-09-22 184411" src="https://github.com/user-attachments/assets/ed6ade66-d8d3-4a12-9ee2-fc989327fa3e" />
alt="GTKWave Example" width="70%">
</div>

---
## 4. Verilog Code Analysis

**The code for the multiplexer (`good_mux.v`):**

```verilog
module good_mux (input i0, input i1, input sel, output reg y);
always @ (*)
begin
    if(sel)
        y <= i1;
    else 
        y <= i0;
end
endmodule
```

###  **How It Works**

- **Inputs:** `i0`, `i1` (data), `sel` (select line)
- **Output:** `y` (registered output)
- **Logic:** If `sel` is 1, `y` gets `i1`; if `sel` is 0, `y` gets `i0`.

---
## 5. Introduction to Yosys & Gate Libraries

### What is Yosys?

Yosys is a powerful, open-source synthesis tool that converts your Verilog design into a gate-level netlist—essentially a blueprint for real hardware.

### 🔹 Why Do Libraries Have Different Gate "Flavors"?

A .lib file isn’t just a single version of a gate—it’s a collection of gate variants, each designed for specific trade-offs. Different gates in a library help the synthesis tool choose the best fit for your circuit’s needs. Here’s what they offer:

⚡ **Performance:** Fast gates for timing-critical paths, slower ones for energy efficiency

🔋 **Power:** Low-power gates to save energy and reduce heat

🏗️ **Area:** Compact gates to make your chip smaller and more efficient

💪 **Drive Strength:** Strong gates to drive larger loads or multiple signals

🌐 **Signal Integrity:** Specialized gates to maintain clean signals in noisy environments

🧩 **Mapping Flexibility:** Synthesis tools pick the most suitable “flavor” for your design goals

Think of it like choosing the right ingredient for a recipe—some are faster, some are lighter, some are stronger—but together they make the perfect dish! 🍲✨
## 6. Synthesis Lab with Yosys

Let’s synthesize the `good_mux` design using Yosys!

###  Step-by-Step Yosys Flow

1. **Start Yosys**
    ```shell
    yosys
    ```
    

2. **Read the liberty library**
    ```shell
    read_liberty -lib /home/pandiyarajans/VLSI/verilog_files/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    ```

3. **Read the Verilog code**
    ```shell
    read_verilog /home/vsduser/VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files/good_mux.v
    ```

4. **Synthesize the design**
    ```shell
    synth -top good_mux
    ```

5. **Technology mapping**
    ```shell
     abc -liberty /home/pandiyarajans/VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    ```


6. **Visualize the gate-level netlist**
    ```shell
    show
    ```
    **output
    <div align="center">
<img width="615" height="350" alt="Screenshot 2025-09-23 230606" src="https://github.com/user-attachments/assets/a5d4bfed-5264-482a-b236-ae350ce5272a" /></div>
## 7. Summary

- I learned about simulators, designs, and testbenches.
- I ran your first Verilog simulation with iverilog and visualized waveforms.
- I analyzed the 2-to-1 mux code.
- I explored Yosys and learned why gate libraries have various flavors.


---



