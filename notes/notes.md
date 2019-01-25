------------------------------------------------------------
Use constructions like  
` (a) public SomeType A { get; } = new SomeType();`
instead of   
`(b) public SomeType B => new SomeType();`  
in cases where SomeType is not an elementary type, otherwise use (b) instead of (a).
If SomeType is not an elementary then in case (a) you'l have only one instance of it, in case (b) new instance will be created in every of property calling. 

But, if SomeType is an elementary then in case (a) your class/struct will be on one field bigger, then in case (b), and it's not necessary.

		
Code
```C#
public class Class1
	{
		public bool A { get; } = false;
		public bool B => false;
	}
```
compiles into:
```IL
.class public auto ansi beforefieldinit 
  ClassLibrary2.Class1
    extends [mscorlib]System.Object
{

  .field private initonly bool '<A>k__BackingField'
  .custom instance void [mscorlib]System.Runtime.CompilerServices.CompilerGeneratedAttribute::.ctor() 
    = (01 00 00 00 )
  .custom instance void [mscorlib]System.Diagnostics.DebuggerBrowsableAttribute::.ctor(valuetype [mscorlib]System.Diagnostics.DebuggerBrowsableState) 
    = (01 00 00 00 00 00 00 00 ) // ........
    // int32(0) // 0x00000000

  .method public hidebysig specialname instance bool 
    get_A() cil managed 
  {
    .custom instance void [mscorlib]System.Runtime.CompilerServices.CompilerGeneratedAttribute::.ctor() 
      = (01 00 00 00 )
    .maxstack 8

    // [11 18 - 11 22]
    IL_0000: ldarg.0      // this
    IL_0001: ldfld        bool ClassLibrary2.Class1::'<A>k__BackingField'
    IL_0006: ret          

  } // end of method Class1::get_A

  .method public hidebysig specialname instance bool 
    get_B() cil managed 
  {
    .maxstack 8

    // [12 19 - 12 24]
    IL_0000: ldc.i4.0     
    IL_0001: ret          

  } // end of method Class1::get_B

```
------------------------------------------------------------
