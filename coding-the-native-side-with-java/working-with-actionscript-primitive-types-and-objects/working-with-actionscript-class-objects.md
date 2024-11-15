# Working with ActionScript Class objects

In your FREFunction implementations, an input parameter can correspond to an
ActionScript class object. The
[FREObject](../../android-java-api-reference/classes/freobject.md) class
provides functions for accessing the ActionScript-defined properties and methods
of the object:

- `getProperty( String propertyName )`

- `setProperty( String propertyName, FREObject value )`

- `callMethod( String propertyName, FREObject[] methodArgs )`

If an output parameter or return value corresponds to an ActionScript class
object, you create the ActionScript object using a static FREObject factory
method:

    FREObject newObject ( String className, FREObject constructorArgs[] )

> **Note:** These general ActionScript object manipulation functions apply to
> all ActionScript class objects. However, the ActionScript classes Array,
> Vector, ByteArray, and BitmapData are special cases because they each involve
> large amounts of data. Therefore, the Java API provides additional specific
> classes for manipulating objects of these special cases.
