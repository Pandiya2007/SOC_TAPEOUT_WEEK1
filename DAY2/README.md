# Day 2: Timing Libraries, Synthesis Approaches, and Efficient Flip-Flop Coding

Welcome to Day 2 of the RTL Workshop. This day covers three crucial topics:
- Understanding the `.lib` timing library (sky130_fd_sc_hd__tt_025C_1v80.lib) used in open-source PDKs.
- Comparing hierarchical vs. flat synthesis methods.
- Exploring efficient coding styles for flip-flops in RTL design.

---
# 📘 Contents  

- ⚡ [**Timing Libraries**](#timing-libraries)  
  - 🔍 [SKY130 PDK Overview](#sky130-pdk-overview)  
  - 🧩 [Decoding `tt_025C_1v80` in SKY130 PDK](#decoding-tt_025c_1v80-in-the-sky130-pdk)  
  - 📂 [Opening & Exploring the `.lib` File](#opening-and-exploring-the-lib-file)  

- 🏗️ [**Hierarchical vs. Flattened Synthesis**](#hierarchical-vs-flattened-synthesis)  
  - 🏢 [Hierarchical Synthesis](#hierarchical-synthesis)  
  - 🏞️ [Flattened Synthesis](#flattened-synthesis)  
  - ⚖️ [Key Differences](#key-differences)  

- 🔄 [**Flip-Flop Coding Styles**](#flip-flop-coding-styles)  
  - ⏱️ [Asynchronous Reset D Flip-Flop](#asynchronous-reset-d-flip-flop)  
  - ⬆️ [Asynchronous Set D Flip-Flop](#asynchronous-set-d-flop)  
  - 🕹️ [Synchronous Reset D Flip-Flop](#synchronous-reset-d-flop)  

- 🛠️ [**Simulation & Synthesis Workflow**](#simulation-and-synthesis-workflow)  
  - 🖥️ [Icarus Ver]()
