# C# Internals

## C# compilation pipeline
C# batch compiler csc.exe
Input:
Code files .cs
References and assemblies exe, dll
Compiler flags /target, /optimize, /debug
Output
Assemblies (exe, dll)
.NET modules (.netmodule)
Windows Runtime modules (.winmd)

## Developer productivity tools
VS (.csproj)
     MSBuild


`csc.exe /nologo hello.cs`

`ildasm.exe hello.exe`

Visual Studio Tools

**ildasm.exe hello.exe**

```msil
.method private hidebysig static void  Main() cil managed
{
  .entrypoint
  // Code size       13 (0xd)
  .maxstack  8
  IL_0000:  nop  DPOL: not optimized build
  IL_0001:  ldstr      "Hello, World!"
  IL_0006:  call       void [mscorlib]System.Console::WriteLine(string)
  IL_000b:  nop
  IL_000c:  ret
} // end of method Program::Main

.method public hidebysig specialname rtspecialname
        instance void  .ctor() cil managed
{
  // Code size       8 (0x8)
  .maxstack  8
  IL_0000:  ldarg.0
  IL_0001:  call       instance void [mscorlib]System.Object::.ctor()
  IL_0006:  nop
  IL_0007:  ret
} // end of method Program::.ctor
```

**ildasm /out=hello.il hello.exe**

```

//  Microsoft (R) .NET Framework IL Disassembler.  Version 4.6.1055.0
//  Copyright (c) Microsoft Corporation.  All rights reserved.



// Metadata version: v4.0.30319
.assembly extern mscorlib
{
  .publickeytoken = (B7 7A 5C 56 19 34 E0 89 )                         // .z\V.4..
  .ver 4:0:0:0
}
.assembly hello
{
  .custom instance void [mscorlib]System.Runtime.CompilerServices.CompilationRelaxationsAttribute::.ctor(int32) = ( 01 00 08 00 00 00 00 00 ) 
  .custom instance void [mscorlib]System.Runtime.CompilerServices.RuntimeCompatibilityAttribute::.ctor() = ( 01 00 01 00 54 02 16 57 72 61 70 4E 6F 6E 45 78   // ....T..WrapNonEx
                                                                                                             63 65 70 74 69 6F 6E 54 68 72 6F 77 73 01 )       // ceptionThrows.

  // --- The following custom attribute is added automatically, do not uncomment -------
  //  .custom instance void [mscorlib]System.Diagnostics.DebuggableAttribute::.ctor(valuetype [mscorlib]System.Diagnostics.DebuggableAttribute/DebuggingModes) = ( 01 00 07 01 00 00 00 00 ) 

  .hash algorithm 0x00008004
  .ver 0:0:0:0
}
.module hello.exe
// MVID: {9B0094D2-6E1A-465E-A23A-866496047702}
.imagebase 0x00400000
.file alignment 0x00000200
.stackreserve 0x00100000
.subsystem 0x0003       // WINDOWS_CUI
.corflags 0x00000001    //  ILONLY
// Image base: 0x00FE0000


// =============== CLASS MEMBERS DECLARATION ===================

.class private auto ansi beforefieldinit Program.Program
       extends [mscorlib]System.Object
{
  .method private hidebysig static void  Main() cil managed
  {
    .entrypoint
    // Code size       13 (0xd)
    .maxstack  8
    IL_0000:  nop
    IL_0001:  ldstr      "Hello, Pluralsight!"
    IL_0006:  call       void [mscorlib]System.Console::WriteLine(string)
    IL_000b:  nop
    IL_000c:  ret
  } // end of method Program::Main

  .method public hidebysig specialname rtspecialname 
          instance void  .ctor() cil managed
  {
    // Code size       8 (0x8)
    .maxstack  8
    IL_0000:  ldarg.0
    IL_0001:  call       instance void [mscorlib]System.Object::.ctor()
    IL_0006:  nop
    IL_0007:  ret
  } // end of method Program::.ctor

} // end of class Program.Program


// =============================================================

// *********** DISASSEMBLY COMPLETE ***********************
// WARNING: Created Win32 resource file hello.res

```

**ilasm hello.il**              
```                                                                    
Microsoft (R) .NET Framework IL Assembler.  Version 4.6.1038.0      
Copyright (c) Microsoft Corporation.  All rights reserved.          
Assembling 'hello.il'  to EXE --> 'hello.exe'                       
Source file is ANSI                                                 
                                                                    
Assembled method Program.Program::Main                              
Assembled method Program.Program::.ctor                             
Creating PE file                                                    
                                                                    
Emitting classes:                                                   
Class 1:        Program.Program                                     
                                                                    
Emitting fields and methods:                                        
Global                                                              
Class 1 Methods: 2;                                                 
                                                                    
Emitting events and properties:                                     
Global                                                              
Class 1                                                             
Writing PE file                                                     
Operation completed successfully                                    
```

hello.exe

Hello, Pluralsight!

**ILSpy**

Download Debugging tools for Windows (SDKSETUP.EXE)

**Inspecting runtime state**
- state of C# Program
- data structures of the runtime (CLR)

**VS debugger** 
- stepping
- conrtrolling
- expression evaluation (Watch, Immediate)

**Native code debugger**
- Debugging tools for Windows downloading
- WinDbg.exe and cdb.exe
- SOS, PSSCOR4, SOSEX, CLRMD debugger extention

**Ex:**
```
cdb.exe hello.exe
sxe clrjit; g
.loaddby sos clr 
!bpmd hello.exe Program.Main
g
```

**WinDbg**
```
File->Open Executable (Ctrl+E)
sxe ld clrjit
g
!help
???
```