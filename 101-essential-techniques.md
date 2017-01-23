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

