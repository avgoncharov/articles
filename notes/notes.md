------------------------------------------------------------
Всегда для константных свойств использовать запись вида:
`public bool B => false;`
вместо `public bool A { get; } = false;`.
		
Код
```C#
public class Class1
	{
		public bool A { get; } = false;
		public bool B => false;
	}
```
Компилируется в:
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
