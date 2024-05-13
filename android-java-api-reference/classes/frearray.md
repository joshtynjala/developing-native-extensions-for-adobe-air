# FREArray

Package:  
com.adobe.fre

Inheritance  
[FREObject](./freobject.md)

Runtime version  
AIR 3

The FREArray class represents an ActionScript Array or Vector object.

| Method                                                                             | Description                                           |
| ---------------------------------------------------------------------------------- | ----------------------------------------------------- |
| public static FREArray newArray (String classname, int numElements, boolean fixed) | Creates an ActionScript Vector array object.          |
| public static FREArray newArray (int numElements)                                  | Creates an ActionScript Array object.                 |
| public long getLength()                                                            | Gets the number of elements in the array.             |
| public void setLength( long length )                                               | Changes the array length.                             |
| public FREObject getObjectAt( long index )                                         | Gets the object at the specified index.               |
| public void setObjectAt( long index, FREObject value )                             | Puts an object into the array at the specified index. |

Methods

You can work with an FREArray object using the methods defined in the FREArray
class, as well as the methods defined in the FREObject class (which is the
FREArray's super class). Use the FREObject `getProperty()` and `setProperty()`
methods to access or modify the ActionScript-defined properties of the Array and
Vector classes. Use `callMethod()` to call the ActionScript-defined methods.

## Method details

#### newArray

    public static FREArray newArray (String classname, int numElements, boolean fixed)

Creates an ActionScript Vector array object.

**Parameters:**

`classname`  
The fully-qualified name of the ActionScript class of the members of the Vector
array.

`numElements`  
The number of elements to allocate for the array.

`fixed`  
If `true`, the vector length cannot be changed.

**Returns:**

`FREArray`  
An FREArray object associated with an ActionScript Vector array object.

**Example:**

    FREArray vector = FREArray.newArray( "flash.geom.Matrix3D", 4, true );

#### newArray

    public static FREArray newArray (int numElements)

Creates an ActionScript Array object.

**Parameters:**

`numElements`  
The number of elements to allocate for the array. The elements are undefined.

**Returns:**

`FREArray`  
An FREArray object associated with an ActionScript Array object.

**Example:**

    FREArray array = FREArray.newArray( 4 );

#### getLength

    public long getLength()

Gets the number of elements in the array.

**Returns:**

`long`  
The length of the array.

**Example:**

    long length = asArray.getLength();

#### setLength

    public void setLength( long length )

Changes the length of this array. If the new length is shorter than the current
length, the array is truncated.

**Parameters:**

`length`  
The new length for the array.

**Example:**

    asArray.setLength( 4 );

#### getObjectAt

    public FREObject getObjectAt( long index )

Gets an element from the array.

**Parameters:**

index  
The position of the element to retrieve. (0-based)

**Returns:**

`FREObject`  
The FREObject instance associated with the ActionScript object in the array.

**Example:**

    FREObject element = asArray.getObjectAt( 2 );

#### setObjectAt

    public void setObjectAt( long index, FREObject value )

Puts an object into the array at the specified index.

**Parameters:**

`index`  
The position in the array at which to put the object. (0-based)

`value`  
An FREObject containing the primitive value or ActionScript object to insert.

**Example:**

    FREObject stringElement = FREObject.newObject("String element value");
    FREArray asVector = FREArray.newArray( "String", 1, false );
    asVector.setObjectAt( 0, stringElement );
