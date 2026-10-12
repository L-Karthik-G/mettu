---
title: "MLIR in Quantum Compilation"
date: "2026-10-11"
---
Recently, I have been working on a cool project called **NQOS(No Quantam Of Solace)** which is esentialy is trying to build a testing framework for the **MQT-CC(Munich Quantum Toolkit- Compiler Collection)** , don’t worry it’s not as cool as it sounds

While i was literature reviewing(idk if its a real phrase) about it, I thought, *"How can I really work on quantam compilers if don’t even know anything about classical compilers"* , Atleast something relevant, I dont wanna go down an another rabbit hole.

Hence I tried to learn about MLIR(Multi level intermediate representaion) which seems to have a decent contribution in both compiling systems and also because it sound cool

## Compilers in general
Before we get into intimidating sounding stuff let’s talk about compilers in general. A compiler need to represent the program internally so that it can do optimisations and fine-turning within itself.

**LLVM which is a compiler stack uses IR (intermediate representation) for this where as JVM uses bytecode - a oops based system with garbage collector**

Other languages like *Rust* or *Swift* also use their own IR versions but it’s not as optimised as lower level representation systems

All of the ablove mentioned representation systems are single-level representations. **"So what could a multilevel representation do better?"**

### MLIR

MLIR which works by extraction in multiple levels hence the name, works on a principle of **"progressive lowering"** by extracting at multiple levels it allows fine-tuning and optimisation at each level although it’s not nesseccary but it’s a nice choice to have. This helps compilation from program code to hardware representation hence  the "progressive lowering".


## MLIR in Quantam Compiling!!

Now that all the yap is done how does it work for my use case? good question. Quantum compilers have historically had 2 approaches . 

A Quantum first approach, which prioritised quantum level gate function and representation but lacked in error correction and optimisation. Classical first  approach is basically the reverese of it 

MQT-CC is a more hybrid approach by treating Quantum Computing as a seperate computing system but eventual accelerator to HPC(high performance computers) this works hand in hand as they are classical limitations to quantam systems 

This part is more technically but is relevant to my application . 

In MQT-CC , MLIR is especially usefull because of its **dialects**. dialects are specialised set operations which can be applied at different layers for layerwise optimisation and compilation as mentioned before (if youb payed attention)

its dialects consist of:

- QC (helps intereact with normal user-level languages)
- QCO (used for quantum program optimisations)
- CBit (represents clasical bit registers with qbit operation)
