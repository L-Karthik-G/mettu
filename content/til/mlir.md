---
title: "MLIR in Quantum Compilation"
date: "2026-10-11"
---

Recently as of this post I have been working on a project where my team and I are trying to build an automated testing framework for the MQT Compiler Collection for the **PES INNOVATION LAB**. 

MQT-CC uses **MLIR(Multi-Level Intermediate Representation)** as one of its innovative factors claiming to bridge the gap between classical-first and quantum-first apporaches at quantum compiler design.

I thought this could be a good first actual post to write about since I have never actually payed attention to deep compiler architecture before and this seems like a fun way to start!

### What is MLIR?

Traditional compiler infrastructures like *LLVM*(basically the compiler backend or source for most program languages) or *JVM*(JAVA virtual machine) have a "one size fits all" approach. which essential means that they rely on a single abstraction layer. 

For example, LLVM uses LLVM Itermediete Represntaion(IR), a low-level assembly-like representation. JVM uses bytecode, a comparitvly higher-level, stack-like, object-oriented type system with a garbage collector abstraction.

Other languages have their own recipes for abstraction for their own domain-specific problems, like language or library-specific optimization by implementing their own native IR, such as *Swift* or *Rust*. However, for most of these languages quality of infrastructre is usually sub-par, which can lead to issues such as slower compile times or buggy compilation.

This is where MLIR comes in. MLIR stands for *Multi-Level Intermediate Representation*, which works on the principle of "Progressive Lowering." It has multiple abstraction layers, which helps it start at a "higher level", from the user code, closer to the source code,helping it do different optimizations at each layer,for the next layers. It helps link multiple "dialects" through its multi-level representation.

### Before MLIR in Quantum Compilation

Before MLIR was adopted in the quantum compiling stack by MQT, there were two main approaches to quantum compilation. The first was a "*quantum-first approach*," which prioritized the quantum-level abstraction as the primary goal and tried to build around it.

However, this approach struggled because of the lack of features like error correction, optimization, and finer control which require classical methods that are not naturally expressed at the quantum level.

The second method was a "*classical-first approach*", which started from a more classical perspective and tried to accelerate quantum compilation. Examples include NVIDIA's CUDA-Q and LLVM-based efforts. However, this approach lacked the domain-specific quantum expertise and optimizations that quantum-first tools had accumulated over years of research.

### MLIR in Quantum Compilation

This is where a hybrid approach emerged: thinking of quantum computing as an independent but eventual accelerator to HPC (High-Performance Computing), similar to GPUs. Hence MLIR was adopted as the main Intermediate Representation method, alongside *QIR(Quantum Intermediete Representation)*. 

MLIR has it's main advantage accociated to the fact that it can deal with dilects at variours levels of abstraction. hence allowing for  seamless composition of compilation passes within a shared infrastructure.

While LLVM excels at low-level optimizations, it lacks mechanisms for representing higher-level program structure or domain-specific semantics. The MLIR framework extends LLVM by introducing a multi-level approach that supports multiple abstraction layers within one infrastructure. 
 
In realtion to MQT-CC,MLIR is used in the middle->end layer where as mentioned before, its multi level abstraction approach helps it split it the program  in a manner that allows  multiple target agnostic approches to work indepdently on their optimization.