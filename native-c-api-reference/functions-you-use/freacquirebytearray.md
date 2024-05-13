# FREAcquireByteArray()

#### Usage

    FREResult FREAcquireByteArray (
            FREObject                 object,
            FREByteArray*                 byteArrayToSet
    );

#### Parameters

object  
An FREObject. This FREObject parameter represents an ActionScript ByteArray
class object.

byteArrayToSet  
A pointer to a variable of type FREByteArray. The runtime sets the fields of
this structure when the native C implementation calls this method. See
[FREByteArray](../structure-typedefs/frebytearray.md).

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded. The FREByteArray parameter is set. The ActionScript
ByteArray object is available for you to manipulate.

FRE_ILLEGAL_STATE  
The extension context has already acquired an ActionScript BitmapData or
ByteArray object. The context cannot call this method until it releases that
BitmapData or ByteArray object.

FRE_INVALID_ARGUMENT  
The `byteArrayToSet` parameter is `NULL`.

FRE_INVALID_OBJECT  
The FREObject `object` parameter is invalid.

FRE_TYPE_MISMATCH  
The FREObject `object` parameter does not represent an ActionScript ByteArray
class object.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to acquire the bytes of an ActionScript ByteArray class
object. Once you have successfully called this function, you cannot successfully
call any other C API function until you call `FREReleaseByteArray()`. This
prohibition is because other calls could, as a side effect, execute code that
invalidates the pointer to the byte array contents.

After calling this function, you can manipulate the bytes of the ByteArray
object. The bytes are available in the `byteArrayToSet` parameter, along with
the number of bytes. When you have finished working with the bytes, call
`FREReleaseByteArray()`.

More Help topics

[FREReleaseByteArray()](./frereleasebytearray.md)
