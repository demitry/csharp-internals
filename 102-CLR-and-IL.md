### 01. Introduction to Intermediate Language (IL)
- CLR internals and IL instructions

**Check out our course catalog!**
- CLR Fundamentals, by Mike Woodring
- MSIL for the C# Developer, by Filip Ekberg

**Books**
- CLR via C#, Jeffrey Richter
- Expert .NET 2.0 IL Assembler, Serge Lidin
- Shared Source CLI 2.0 Internals, Joel Poebar & Ted Neward

**Intermediate Language (IL)**
- Virtual Machine language of the CLR
  - Emitted by managed language compilers (C#, VB, F#, etc.)
  - NGEN or JIT compiled to native code
- Stack-based evaluation
  - No registers
  - Locals, arguments, fields, etc.
- Verification
  - Type safe
  - Memory safe
- Leverages metadata

**Stack-based evaluation**
- “Scratch-pad” for computation
- Pop operands, execute operator, push result
- Each instruction has a net effect on the stack
- E.g. add = 2 x pop +1 x push
- Stack transitions for “1 + 2

```
ldc.i4.1
ldc.i4.2
add
```

### 02. Essential IL Instructions
### 03. Local Variables in IL
### 04. Basic IL Instructions and Branches
### 05. Analyzing Branches in ILDASM
### 06. Call Instructions and Call Stacks
### 07. Exceptions, Objects, and Arrays
### 08. The Role of JIT Compilation
### 09. Seeing JIT Compilation in Action in WinDbg
### 10. JIT Optimizations
### 11. Summary