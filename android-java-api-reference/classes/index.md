# Classes

The Java API for AIR native extensions defines one abstract class, FREContext,
that allows you to define the extension context. The API also defines several
concrete classes, FREObject and its subclasses, which represent objects shared
between the Java and ActionScript sides of a native extension. An extension must
implement at least one concrete subclass of FREContext.

- [FREArray](./frearray.md)
- [FREByteArray](./frebytearray.md)
- [FREBitmapData](./frebitmapdata.md)
- [FREContext](./frecontext.md)
- [FREObject](./freobject.md)
