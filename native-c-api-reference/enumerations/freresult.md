# FREResult

The FREResult enumeration defines return values for native extensions C API
functions you call.

    enum FREResult {
        FRE_OK                         = 0,
        FRE_NO_SUCH_NAME               = 1,
        FRE_INVALID_OBJECT             = 2,
        FRE_TYPE_MISMATCH              = 3,
        FRE_ACTIONSCRIPT_ERROR         = 4,
        FRE_INVALID_ARGUMENT           = 5,
        FRE_READ_ONLY                  = 6,
        FRE_WRONG_THREAD               = 7,
        FRE_ILLEGAL_STATE              = 8,
        FRE_INSUFFICIENT_MEMORY        = 9,
        FREResult_ENUMPADDING          = 0xffff
    };

The enumeration values have the following meanings:

FRE_OK  
The function succeeded.

FRE_ACTIONSCRIPT_ERROR  
An ActionScript error occurred, and an exception was thrown. The C API functions
that can result in this error allow you to specify an FREObject to receive
information about the exception.

FRE_ILLEGAL_STATE  
A call was made to a native extensions C API function when the extension context
was in an illegal state for that call. This return value occurs in the following
situation. The context has acquired access to an ActionScript BitmapData or
ByteArray class object. With one exception, the context can call no other C API
functions until it releases the BitmapData or ByteArray object. The one
exception is that the context can call `FREInvalidateBitmapDataRect()` after
calling `FREAcquireBitmapData()` or `FREAcquireBitmapData2()`.

FRE_INSUFFICIENT_MEMORY  
The runtime could not allocate enough memory to change the size of an Array or
Vector object.

FRE_INVALID_ARGUMENT  
A pointer parameter is `NULL`.

FRE_INVALID_OBJECT  
An FREObject parameter is invalid. For examples of invalid FREObject variables,
see
[FREObject validity](../../coding-the-native-side-with-c/the-freobject-type.md#freobject-validity).

FRE_NO_SUCH_NAME  
The name of a class, property, or method passed as a parameter does not match an
ActionScript class name, property, or method.

FRE_READ_ONLY  
The function attempted to modify a read-only property of an ActionScript object.

FRE_TYPE_MISMATCH  
An FREObject parameter does not represent an object of the ActionScript class
expected by the called function.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

FREResult_ENUMPADDING  
This final enumeration value is to guarantee that the size of an enumeration
value is always 4 bytes.
