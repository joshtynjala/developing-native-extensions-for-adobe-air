# Working with ActionScript ByteArray objects

Use the ActionScript ByteArray class to efficiently pass many bytes between the
ActionScript side and Java side of your extension. The
[FREByteArray](../../android-java-api-reference/classes/frebytearray.md) class
extends [FREObject](../../android-java-api-reference/classes/freobject.md) with
methods for handling byte array objects:

- `acquire()`

- `getLength()`

- `getBytes()`

- `release()`

To manipulate the bytes of the ByteArray object in the Java code, use the
FREByteArray `acquire()` method, followed by the `getBytes()` method. After you
have manipulated the bytes, use the FREByteArray `release()` method.

Do not call any FREObject methods (of any object, not just the acquired object)
between the calls to `acquire()` and `release()`. This prohibition is because
other calls could, as a side effect, execute code that invalidates the byte
array object or its contents.

Do not copy more bytes into the `bytes` field of the acquired FREByteArray
object than the `length` field specifies. The ActionScript side will ignore any
extra bytes.

You can create new FREByteArray object with the static factory method,
`FREByteArray.newByteArray()`. The new byte array is empty. To add data to it
from Java, you must first set the ActionScript `length` property:

    FREByteArray freByteArray = freByteArray = FREByteArray.newByteArray();
    freByteArray.setProperty( "length", FREObject.newObject( 12 ) );
    freByteArray.acquire();
    ByteBuffer bytes = freByteArray.getBytes();
    //set the data
    freByteArray.release();
