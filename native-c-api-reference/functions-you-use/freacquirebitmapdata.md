# FREAcquireBitmapData()

#### Usage

    FREResult FREAcquireBitmapData (
            FREObject                 object,
            FREBitmapData*                 descriptorToSet
    );

#### Parameters

object  
An FREObject. This FREObject parameter represents an ActionScript BitmapData
class object.

descriptorToSet  
A pointer to a variable of type FREBitmapData. The runtime sets the fields of
this structure when the native C implementation calls this method. See
[FREBitmapData](../structure-typedefs/frebitmapdata.md).

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded. The FREBitmapData parameter is set. The ActionScript
BitmapData object is available for you to manipulate.

FRE_ILLEGAL_STATE  
The extension context has already acquired an ActionScript BitmapData or
ByteArray object. The context cannot call this method until it releases that
BitmapData or ByteArray object.

FRE_INVALID_ARGUMENT  
The `descriptorToSet` parameter is `NULL`.

FRE_INVALID_OBJECT  
The FREObject `object` parameter is invalid.

FRE_TYPE_MISMATCH  
The FREObject `object` parameter does not represent an ActionScript BitmapData
class object.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to acquire the bitmap of an ActionScript BitmapData class
object. Once you have successfully called this function, you cannot successfully
call any other C API function until you call `FREReleaseBitmapData()`. This
prohibition is because other calls could, as a side effect, execute code that
invalidates the pointer to the bitmap contents.

After calling this function, you can manipulate the bitmap of the BitmapData
object. The bitmap is available in the `descriptorToSet` parameter, along with
other information about the bitmap. To notify the runtime that the bitmap or
subrectangle of the bitmap has changed, call `FREInvalidateBitmapDataRect()`.
When you have finished working with the bitmap, call `FREReleaseBitmapData()`.

More Help topics

[FREReleaseBitmapData()](./frereleasebitmapdata.md)

[FREInvalidateBitmapDataRect()](./freinvalidatebitmapdatarect.md)
