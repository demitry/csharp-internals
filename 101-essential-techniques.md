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

```msil
ildasm.exe hello.exe
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

**ILSpy**

ilasm /exe hello.il

Microsoft (R) .NET Framework IL Assembler.  Version 4.6.1586.0
Copyright (c) Microsoft Corporation.  All rights reserved.
Assembling 'hello.il'  to EXE --> 'hello.exe'
Source file is ANSI

Assembled method HelloWorld.Hello::Main
Assembled method HelloWorld.Hello::.ctor
Creating PE file

Emitting classes:
Class 1:        HelloWorld.Hello

Emitting fields and methods:
Global
Class 1 Methods: 2;

Emitting events and properties:
Global
Class 1
Writing PE file
Operation completed successfully


