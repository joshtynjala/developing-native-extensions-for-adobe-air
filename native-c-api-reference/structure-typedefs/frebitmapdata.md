# FREBitmapData

Use the FREBitmapData or FREBitmapData2 structures when acquiring and
manipulating the bits in an ActionScript BitmapData class object. The
FREBitmapData structure is defined as follows:

    typedef struct {
        uint32_t            width;
        uint32_t            height;
        uint32_t            hasAlpha;
        uint32_t            isPremultiplied;
        uint32_t            lineStride32;
        uint32_t*           bits32;
    } FREBitmapData;

The fields of FREBitmapData have the following meanings:

width  
A uint32_t that specifies the width, in pixels, of the bitmap. This value
corresponds to the `width` property of the ActionScript BitmapData class object.
This field is read-only.

height  
A uint32_t that specifies the height, in pixels, of the bitmap. This value
corresponds to the `height` property of the ActionScript BitmapData class
object. This field is read-only.

hasAlpha  
A uint32_t that indicates whether the bitmap supports per-pixel transparency.
This value corresponds to the `transparent` property of the ActionScript
BitmapData class object. If the value is non-zero, then the pixel format is
`ARGB32`. If the value is zero, the pixel format is `_RGB32`. Whether the value
is big endian or little endian depends on the host device. This field is
read-only.

isPremultiplied  
A uint32*t that indicates whether the bitmap pixels are stored as premultiplied
color values. A non-zero value means the values \_are* premultipled. This field
is read-only. For more information about premultiplied color values, see
BitmapData.getPixel() in the
_[ActionScript 3.0 Reference for the Adobe Flash Platform](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/index.html)_.

lineStride32  
A uint32_t that specifies the number of uint32_t values per scanline. This value
is typically the same as the `width` parameter. This field is read-only.

bits32  
A pointer to a uint32_t. This value is an array of uint32_t values. Each value
is one pixel of the bitmap.

> **Note:** The only field of a `FREBitmapData` structure that you can change in
> the native implementation is the `bits32` field. The `bits32` field contains
> the actual bitmap values. Treat all the other fields in the `FREBitmapData`
> structure as read-only fields.

More Help topics

[FREBitmapData2](./frebitmapdata2.md)

[FREAcquireBitmapData()](../functions-you-use/freacquirebitmapdata.md)

[FREInvalidateBitmapDataRect()](../functions-you-use/freinvalidatebitmapdatarect.md)
