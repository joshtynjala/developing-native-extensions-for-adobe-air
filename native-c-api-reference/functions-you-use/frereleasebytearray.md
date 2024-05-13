# FREReleaseByteArray()

#### Usage

    FREResult FREReleaseByteArray (FREObject object);

#### Parameters

object  
An FREObject that corresponds to an ActionScript ByteArray class object.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded. The ActionScript ByteArray object is no longer available
for you to manipulate.

FRE_ILLEGAL_STATE  
The extension context has not acquired the ActionScript ByteArray object.

FRE_INVALID_OBJECT  
The FREObject `object` parameter is invalid.

FRE_TYPE_MISMATCH  
The FREObject `object` parameter does not correspond to an ActionScript
ByteArray object.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to release an ActionScript ByteArray class object. Before
calling this function, call `FREAcquireByteArray()`. After calling this
function, you can no longer manipulate the ByteArray bytes, but you can again
call other native extension C API functions.

More Help topics

[FREAcquireByteArray()](./freacquirebytearray.md)
