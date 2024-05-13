# FREInvalidateBitmapDataRect()

#### Usage

    FREResult FREInvalidateBitmapDataRect(
            FREObject object,
            uint32_t x,
            uint32_t y,
            uint32_t width,
            uint32_t height
    );

#### Parameters

object  
An FREObject that represents a previously acquired ActionScript BitmapData class
object.

x  
A uint32_t. This value is the x coordinate in terms of pixels. The value is
relative to the upper-left corner of the bitmap. Along with the `y` parameter,
it indicates the upper-left corner of the rectangle to invalidate.

y  
A uint32_t. This value is the y coordinate in terms of pixels. The value is
relative to the upper-left corner of the bitmap. Along with the `x` parameter,
it indicates the upper-left corner of the rectangle to invalidate.

width  
A uint32_t. This value is the width in pixels of the rectangle to invalidate.

height  
A uint32_t. This value is the height in pixels of the rectangle to invalidate.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded. The specified rectangle has been invalidated.

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

Call this function to invalidate a rectangle of an ActionScript BitmapData class
object. Before calling this function, call `FREAcquireBitmapData()` or
`FREAcquireBitmapData2()`. Call `FREReleaseBitmapData()` after you are done
manipulating and invalidating the bitmap.

Invalidating a rectangle of a BitmapData object indicates to the runtime that it
will need to redraw the rectangle.

More Help topics

[FREAcquireBitmapData()](./freacquirebitmapdata.md)

[FREAcquireBitmapData2()](./freacquirebitmapdata2.md)

[FREReleaseBitmapData()](./frereleasebitmapdata.md)
