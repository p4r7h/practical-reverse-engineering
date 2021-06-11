1. Repeat the walk-through by yourself. Draw the stack layout, including parameters and local variables. 

2. In the example walk-through, we did a nearly one-to-one translation of the assembly code to C. As an exercise, re-decompile this whole function so that it looks more natural. What can you say about the developer's skill level/experience? Explain your reasons. Can you do a better job? 

3. In some of the assembly listings, the function name has a @ prefix followed by a number. Explain when and why this decoration exists. 

4. Implement the following functions in x86 assembly: strlen , strchr , memcpy , memset , strcmp , strset . 

5. Decompile the following kernel routines in Windows: 
```
KeInitializeDpc 
KeInitializeApc 
ObFastDereferenceObject (and explain its calling convention) 
KeInitializeQueue 
KxWaitForLockChainValid 
KeReadyThread 
KiInitializeTSS 
RtlValidateUnicodeString
```

6. Sample H . The function sub_13846 references several structures whose types are not entirely clear. 
Your task is to first recover the function prototype and then try to reconstruct the structure fields. 
After reading Chapter 3, return to this exercise to see if your understanding has changed. 
(Note: This sample is targeting Windows XP x86.)

7. Sample H . The function sub_10BB6 has a loop searching for something. First recover the function prototype and then infer the types based on the context.
Hint: You should probably have a copy of the PE specification nearby.

8. Sample H . Decompile sub_11732 and explain the most likely programming construct used in the original code.

9. Sample L . Explain what function sub_1000CEA0 does and then decompile it back to C.

10. If the current privilege level is encoded in CS, which is modifiable by user-mode code, why can't user-mode code modify CS to change CPL?

11. Read the Virtual Memory chapter in Intel Software Developer Manual , Volume 3 and AMD64 Architecture Programmer's Manual , 
Volume 2 : System Programming . Perform a few virtual address to physical address translations yourself and verify the result with a kernel debugger. 
Explain how data execution prevention (DEP) works. 

12. Bruce's favorite x86/x64 disassembly library is BeaEngine by BeatriX ( www.beaengine.org ). 
Experiment with it by writing a program to disassemble a binary at its entry point.
