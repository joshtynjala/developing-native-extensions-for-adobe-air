# FREReleaseBitmapData()

#### Usage

    FREResult FREReleaseBitmapData (FREObject object);

#### Parameters

object  
An FREObject that corresponds to an ActionScript BitmapData class object.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded. The ActionScript BitmapData object is no longer
available for you to manipulate.

FRE_ILLEGAL_STATE  
The extension context has not acquired the ActionScript BitmapData object.

FRE_INVALID_OBJECT  
The FREObject `object` parameter is invalid.

FRE_TYPE_MISMATCH  
The FREObject `object` parameter does not represent an ActionScript BitmapData
class object.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to release an ActionScript BitmapData class object. Before
calling this function, call `FREAcquireBitmapData()` or
`FREAcquireBitmapData2()` and `FREInvalidateBitmapDataRect()`. After calling
this function, you can no longer manipulate the bitmap, but you can again call
other native extension C API functions.

More Help topics

[FREAcquireBitmapData()](./freacquirebitmapdata.md)

[FREAcquireBitmapData2()](./freacquirebitmapdata2.md)

[FREInvalidateBitmapDataRect()](./freinvalidatebitmapdatarect.md)
