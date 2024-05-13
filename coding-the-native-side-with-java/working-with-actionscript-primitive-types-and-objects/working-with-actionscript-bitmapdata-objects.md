# Working with ActionScript BitmapData objects

Use the ActionScript BitmapData class to pass bitmaps between the ActionScript
side and Java side of your extension. The
[FREBitmapData](../../android-java-api-reference/classes/frebitmapdata.md) class
extends FREObject with the following methods appropriate for handling bitmap
data objects:

- `acquire()`

  You must call `acquire()` before calling any other these other methods:

- `getHeight()`

- `getWidth()`

- `hasAlpha()`

- `isInvertedY()` (AIR 3.1)

- `isPremultiplied()`

- `getLineStride32()`

- `getBits()`

- `invalidateRect()`

- `release()`

To change the bitmap data, call `acquire()` and then get the pixel color data
with the `getBits()` method. The `getLineStride32()` method indicates how many
32-bit data are in each horizontal line. Although this value is usually equal to
the width of the bitmap, in some cases bitmap data can be padded with extra,
non-visible bytes. Each pixel in the bitmap is a 32-bit value in ARGB format.
After you have manipulated the bitmap, release the bitmap data by calling
`release()`.

Do not call any FREObject methods (of any object, not just the acquired object)
between the calls to `acquire()` and `release()`. This prohibition is because
other calls could, as a side effect, execute code that invalidates the byte
array object or its contents.

To indicate that the Java implementation has modified all or part of the bitmap,
invalidate a rectangle of the bitmap with the `invalidateRect()` function. The
`x` and `y` parameters are the coordinates of the rectangle to invalidate,
relative to the 0,0 coordinates which are the top, left corner of the bitmap.
The `width` and `height` fields are the dimensions in pixels of the rectangle to
invalidate.

You can create new FREBitmapData object with the static factory method,
`FREBitmapData.newBitmapData()`.
