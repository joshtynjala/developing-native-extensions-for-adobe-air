# FREGetArrayLength()

#### Usage

    FREResult FREGetArrayLength (
            FREObject             arrayOrVector,
            uint32_t*             length
    );

#### Parameters

arrayOrVector  
An FREObject that represents an ActionScript Array or Vector class object.

length  
A pointer to a uint32_t. This method sets the uint32_t variable pointed to by
this parameter with the length of the Array or Vector class object.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded. The method set the uint32_t variable that the `length`
parameter points to. It sets the variable to the length of the Array or Vector
object.

FRE_ILLEGAL_STATE  
The extension context has acquired an ActionScript BitmapData or ByteArray
object. The context cannot call this method until it releases the BitmapData or
ByteArray object.

FRE_INVALID_ARGUMENT  
The `length` parameter is `NULL`.

FRE_INVALID_OBJECT  
The `arrayOrVector` FREObject parameter is invalid.

FRE_TYPE_MISMATCH  
The `arrayOrVector` FREObject parameter does not represent an ActionScript Array
or Vector class object.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to get the length of an Array or Vector class object. The
FREObject parameter `arrayOrVector` represents the Array or Vector object. The
runtime returns the length in the uint32_t variable that the `length` parameter
points to.

More Help topics

[FRESetArrayLength()](./fresetarraylength.md)

[FRESetArrayElementAt()](./fresetarrayelementat.md)
