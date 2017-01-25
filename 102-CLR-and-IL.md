<!-- TOC -->

- [01. Introduction to Intermediate Language (IL)](#01-introduction-to-intermediate-language-il)
- [02. Essential IL Instructions](#02-essential-il-instructions)
- [03. Local Variables in IL](#03-local-variables-in-il)
- [04. Basic IL Instructions and Branches](#04-basic-il-instructions-and-branches)
- [05. Analyzing Branches in ILDASM](#05-analyzing-branches-in-ildasm)
- [06. Call Instructions and Call Stacks](#06-call-instructions-and-call-stacks)
- [07. Exceptions, Objects, and Arrays](#07-exceptions-objects-and-arrays)
- [08. The Role of JIT Compilation](#08-the-role-of-jit-compilation)
- [09. Seeing JIT Compilation in Action in WinDbg](#09-seeing-jit-compilation-in-action-in-windbg)
- [10. JIT Optimizations](#10-jit-optimizations)
- [11. Summary](#11-summary)

<!-- /TOC -->

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
ldc.i4.1  |  |
ldc.i4.2  |__|
add
```

### 02. Essential IL Instructions
**Essential instructions**
- pop
    - Pops the object on top of the stack
    - Often used to discard stuff to rebalance the stack
- dup
    - Duplicates the object on top of the stack
    - Often used to eliminate loads and stores to locals
- nop
    - No-operation, doesn’t do anything “useful”
    - Often used in non-optimized builds (csc/o-)
    - Breakpoints can only be set on instructions
    - E.g. emit nop for lines with curly braces

**Loading constants**
- Numerical:
    - ldc.i4 for “load constant integer 4 bytes” (int)
    - ldc.r8 for “load constant floating point 8 bytes” (double)
    - Value as an operand in the IL instruction stream
    - Shorthand instructions, e.g. ldc.i4.1 for Int32 1, ldc.i4.m1 for Int32 -1
- Boolean:
    - Represented as 0 (false) or 1 (true)
- String:
    - ldstr for “load string”
    - Value as an operand that points to a string table entry
- Null:
    - ldnull
    - Null reference, useful for initialization or cleanup of locations

### 03. Local Variables in IL
**Locals**
- Typed slots to hold objects
- JIT may put those in machine registers or on the stack
- Instructions to load and store
    - E.g. ldloc.0 pushes the 0 th local onto the evaluation stack
    - E.g. stloc.1 pops from the evaluation stack and stores into the 1 st local


```cs
using System;
namespace HelloWorld
{
	class Hello{
		static void Main()
		{
			int x = 42;
			bool b = false;
			double d = Math.PI;
			string s = "Hello";
		}
	}
}

```

```
.method private hidebysig static void  Main() cil managed
// SIG: 00 00 01
{
  .entrypoint
  // Method begins at RVA 0x2050
  // Code size       23 (0x17)
  .maxstack  1
  .locals init (int32 V_0,
           bool V_1,
           float64 V_2,
           string V_3)
  IL_0000:  /* 00   |                  */ nop
  IL_0001:  /* 1F   | 2A               */ ldc.i4.s   42
  IL_0003:  /* 0A   |                  */ stloc.0
  IL_0004:  /* 16   |                  */ ldc.i4.0
  IL_0005:  /* 0B   |                  */ stloc.1
  IL_0006:  /* 23   | 182D4454FB210940 */ ldc.r8     3.1415926535897931
  IL_000f:  /* 0C   |                  */ stloc.2
  IL_0010:  /* 72   | (70)000001       */ ldstr      "Hello"
  IL_0015:  /* 0D   |                  */ stloc.3
  IL_0016:  /* 2A   |                  */ ret
} // end of method Hello::Main
```

**Metainfo**

View -> Metainfo -> Show (Ctrl + M)
```
...
User Strings
-------------------------------------------------------
70000001 : ( 5) L"Hello"
...
```

### 04. Basic IL Instructions and Branches
### 05. Analyzing Branches in ILDASM
### 06. Call Instructions and Call Stacks
### 07. Exceptions, Objects, and Arrays
### 08. The Role of JIT Compilation
### 09. Seeing JIT Compilation in Action in WinDbg
### 10. JIT Optimizations
### 11. Summary