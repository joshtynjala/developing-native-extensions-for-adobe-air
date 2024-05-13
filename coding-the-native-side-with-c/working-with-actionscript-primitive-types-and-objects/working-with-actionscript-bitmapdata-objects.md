# Working with ActionScript BitmapData objects

Use the ActionScript BitmapData class to pass bitmaps between the ActionScript
side and native side of your extension. In your native functions, an input
parameter, output parameter, or return value can correspond to an ActionScript
BitmapData class object.

As with other ActionScript class objects, an FREObject variable is the native
side representation of an ActionScript BitmapData object. The C APIs provide
functions for manipulating a BitmapData class object using an FREObject
variable. Use `FRESetObjectProperty()`, `FREGetObjectProperty()`, and
`FRECallObjectMethod()` to get and set the ActionScript ByteArray object's
properties and to call its methods.

However, to manipulate the bits of the BitmapData object in the native code, use
the C API function
[FREAcquireBitmapData()](../../native-c-api-reference/functions-you-use/freacquirebitmapdata.md)
or
[FREAcquireBitmapData2()](../../native-c-api-reference/functions-you-use/freacquirebitmapdata2.md).
These methods access the bits of a BitmapData object that was created on the
ActionScript side:

    FREResult FREAcquireBitmapData(
        FREObject                     object,
        FREBitmapData*                 descriptorToSet
    );
    // The type FREBitmapData is defined as:

    typedef struct {
        uint32_t            width;
        uint32_t            height;
        bool            hasAlpha;
        bool            isPremultiplied;
        uint32_t            lineStride32;
        uint32_t*            bits32;
    } FREBitmapData;

    //Or:
    FREResult FREAcquireBitmapData2(
        FREObject                     object,
        FREBitmapData2*                 descriptorToSet
    );
    // The type FREBitmapData is defined as:

    typedef struct {
        uint32_t            width;
        uint32_t            height;
        bool            hasAlpha;
        bool            isInvertedY;
        bool            isPremultiplied;
        uint32_t            lineStride32;
        uint32_t*            bits32;
    } FREBitmapData2;

All the fields of a `FREBitmapData` or `FREBitmapData2` structure are read-only.
However, the `bits32` field points to the actual bitmap values, which you can
modify in your native implementation. The `FREBitmapData2` structure and
`FREAquireBitmapData2` function were added to the API in AIR 3.1.
`FREBitmapData2` contains one additional field, `isInvertedY`, which indicates
the order in which the rows of image data are stored.

To indicate that the native implementation has modified all or part of the
bitmap, invalidate a rectangle of the bitmap. Use the C API function
[FREInvalidateBitmapDataRect()](../../native-c-api-reference/functions-you-use/freinvalidatebitmapdatarect.md):

    FREResult FREInvalidateBitmapDataRect(
        FREObject object,
        uint32_t x,
        uint32_t y,
        uint32_t width,
        uint32_t height
    );

The `x` and `y` fields are the coordinates of the rectangle to invalidate,
relative to the 0,0 coordinates which are the top, left corner of the bitmap.
The `width` and `height` fields are the dimensions in pixels of the rectangle to
invalidate.

After you have manipulated the bitmap, use the C API function
[FREReleaseBitmapData()](../../native-c-api-reference/functions-you-use/frereleasebitmapdata.md):

    FREResult FREReleaseBitmapData(FREObject object);

> Note: Do not call any C API function except `FREInvalidateBitmapDataRect()`
> between the calls to `FREAcquireBitmapData()` and `FREReleaseBitmapData()`.
> This prohibition is because other calls could, as a side effect, execute code
> that invalidates the pointer to the bitmap contents.
