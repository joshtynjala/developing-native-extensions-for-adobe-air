# Working with ActionScript Array and Vector objects

Use the ActionScript Vector and Array classes to efficiently pass arrays between
the ActionScript side and Java side of your extension.

The [FREArray](../../android-java-api-reference/classes/frearray.md) class
extends [FREObject](../../android-java-api-reference/classes/freobject.md) with
the following methods appropriate for handling array and vector objects:

- `getLength()`

- `setLength( long length )`

- `getObjectAt( long index )`

- `setObjectAt( long index, FREObject value )`

The FREArray also defines factory methods for creating arrays and vectors:

- `FREArray newArray( int numElements )`

- `FREArray newArray( String classname, int numElements, boolean fixed )`
