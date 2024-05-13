# FREByteArray

Package:  
com.adobe.fre

Inheritance  
[FREObject](./freobject.md)

Runtime version  
AIR 3

The FREByteArray class represents an ActionScript ByteArray object.

| Method                                    | Description                                                                  |
| ----------------------------------------- | ---------------------------------------------------------------------------- |
| public static FREByteArray newByteArray() | Creates an empty ActionScript ByteArray object.                              |
| public long getLength()                   | Returns the length of the byte array in bytes.                               |
| public ByteBuffer getBytes()              | Gets the contents of the ActionScript ByteArray object as a Java ByteBuffer. |
| public void acquire()                     | Acquires a lock on the ActionScript object.                                  |
| public void release()                     | Releases a lock on the ActionScript object.                                  |

Methods

Access the data in the ByteArray object by calling `getBytes()`. Before
accessing the byte data in an array referenced by ActionScript, you must call
`acquire()` to lock the object. After you are done accessing or modifying the
data, call `release()` to release the lock.

While you have a lock on the array, you can modify the existing data in the
buffer, but you cannot change the size of the array. To modify the array size,
release the lock and change the ActionScript-defined `length` property using the
`setProperty()` method (defined by the FREObject super class). You can use the
`getProperty()`, `setProperty()`, and `callMethod()` functions to access any of
the properties and methods defined by the ActionScript ByteArray class.

## Method details

#### newByteArray

    public static FREByteArray newByteArray()

Creates an empty ActionScript ByteArray object and its associated Java
FREByteArray instance.

**Returns:**

`FREByteArray`  
The FREByteArray object representing an ActionScript ByteArray.

**Example:**

    FREBytearray bytearray = FREByteArray.newByteArray();

#### acquire

    public void acquire()

Acquires a lock on this object so that the data cannot be modified or disposed
by the runtime or application code while you are accessing it. When you have a
lock, you cannot read or modify any of the ActionScript-defined properties of
the object.

#### getLength

    public long getLength()

Returns the number of bytes in the byte array. You must call this object's
`acquire()` function before calling this method.

**Returns:**

`long`  
The number of bytes in the byte array.

#### getBytes

    public ByteBuffer getBytes()

Returns the byte data in the array. You must call `acquire()` to lock the object
before calling this method. The buffer is only valid while you have a lock.

`java.nio.ByteBuffer`  
The data in the byte array.

**Example:**

    FREByteArray bytearray = FREByteArray.newByteArray();
    bytearray.acquire();
    ByteBuffer bytes = bytearray.getBytes();
    bytes.putFloat( 16.3 );
    bytearray.release();

#### release

    public void release()

Releases the lock obtained by `acquire()`. You must release the lock before
accessing any FREByteArray properties other than the data returned by
`getBytes()`.
