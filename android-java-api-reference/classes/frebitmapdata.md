# FREBitmapData

Package:  
com.adobe.fre

Inheritance  
[FREObject](./freobject.md)

Runtime version  
AIR 3

The FREBitmapData class represents an ActionScript BitmapData object.

| Method                                                                                                     | Description                                                                    |
| ---------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| public static FREBitmapData newBitmapData (int width, int height, boolean transparent, Byte\[\] fillColor) | Creates an ActionScript BitmapData object.                                     |
| public int getWidth()                                                                                      | Gets the bitmap width.                                                         |
| public int getHeight()                                                                                     | Gets the bitmap height.                                                        |
| public boolean hasAlpha()                                                                                  | Indicates whether the bitmap has an alpha channel.                             |
| public boolean isPremultiplied()                                                                           | Indicates whether the bitmap colors are already multiplied by the alpha value. |
| public int getLineStride32()                                                                               | Gets the number of 32-bit values per bitmap scan line.                         |
| ByteBuffer getBits()                                                                                       | Gets the bitmap pixels.                                                        |
| public void acquire()                                                                                      | Acquires a lock on the ActionScript object.                                    |
| void invalidateRect( int x, int y, int width, int height )                                                 | Marks a rectangle within the bitmap as in need of update.                      |
| public void release()                                                                                      | Releases a lock on the ActionScript object.                                    |
| **Added in AIR 3.1:**                                                                                      |                                                                                |
| public boolean isInvertedY                                                                                 | Indicates the order in which the rows of image data are stored.                |

Methods

Most properties of an FREBitmapData object are read only. For example, you
cannot change the width or height of a bitmap. (To change these properties,
create a new FREBitmapData object with the desired dimensions.) You can,
however, access and modify an existing bitmap's pixel values using the
`getBits()` method. You can also access the ActionScript-defined properties of
the BitmapData object using the [FREObject](./freobject.md) `getProperty()` and
`setProperty()` methods and call the object's ActionScript methods with the
FREObject `callMethod()` function.

Before calling `getBits()` on FREBitmapData object that is referenced by
ActionScript code, lock the bitmap using the `acquire()` method. This prevents
the AIR runtime or the application from modifying or disposing the bitmap object
while your function is running (possibly in another thread). After modifying the
bitmap, call `invalidateRect()` to notify the runtime that the bitmap has
changed and release the lock with `release()`. You cannot use
ActionScript-defined properties and methods while you have acquired a lock.

The AIR runtime defines pixel data as a 32-bit value containing three color
components, plus alpha in the order: ARGB. Each component within the data is one
byte. Valid bitmap data is stored with the color components premultiplied by the
alpha component. (However, it is possible to receive a technically invalid
BitmapData in which the colors have not been premultiplied. For example,
rendering bitmaps with the Context3D class can produce such an invalid bitmap.
In this case, the `isPremultiplied()` method still reports `true`.)

## Method details

#### newBitmapData

    public static FREBitmapData newBitmapData (int width, int height, boolean transparent, Byte[] fillColor)

Creates an FREBitmapData object, which can be returned to the ActionScript side
of the extension as a BitmapData instance.

**Parameters:**

`width`  
The width in pixels. In AIR 3+, there is no arbitrary limit to the width or
height of a bitmap (other than the maximum value of an ActionScript signed
integer). However, practical memory limits still apply. Bitmap data occupies 32
bits of memory per pixel.

`height`  
The height in pixels.

`transparent`  
Specifies whether this bitmap uses the alpha channel. This parameter corresponds
to the `hasTransparency()` method of the created FREBitmapData and the
`transparent` property of the ActionScript BitmapData object.

`fillColor`  
The 32-bit, ARGB color value with which to fill the new bitmap. If the
`transparent` parameter is `false`, the alpha component of the color is ignored.

**Returns:**

`FREBitmapData`  
The FREBitmapData object associated with an ActionScript BitmapData object.

**Example:**

    Byte[] fillColor = {0xf,0xf,0xf,0xf,0xf,0xf,0xf,0xf};
    FREBitmapData bitmap = FREBitmapData.newBitmapData( 320, 200, true, fillColor );

#### getWidth

    public int getWidth()

Returns the width, in pixels, of the bitmap. This value corresponds to the
`width` property of the ActionScript BitmapData class object. You must call this
object's `acquire()` function before calling this method.

**Returns:**

`int`  
the number of pixels across the horizontal axis of the bitmap.

#### getHeight

    public int getHeight()

The height, in pixels, of the bitmap. This value corresponds to the `height`
property of the ActionScript BitmapData class object. You must call this
object's `acquire()` function before calling this method.

**Returns:**

`int`  
The number of pixels across the vertical axis of the bitmap.

#### hasAlpha

    public boolean hasAlpha()

Indicates whether the bitmap supports per-pixel transparency. This value
corresponds to the `transparent` property of the ActionScript BitmapData class
object. If the value is `true`, then the alpha component of the pixel color
values is used. If the value is `false`, the alpha component of the color is not
used. You must call this object's `acquire()` function before calling this
method.

**Returns:**

`boolean`  
true if the bitmap uses an alpha channel.

#### isPremultiplied

    public boolean isPremultiplied()

Indicates whether the bitmap pixels are stored as premultiplied color values. A
true value means the red, green, and blue components of a pixel color _are_
premultiplied by the alpha component. ActionScript BitmapData objects are
currently always premultiplied (but future changes to the runtime could make it
possible to create a bitmap that is not premultiplied). For more information
about premultiplied color values, see BitmapData.getPixel() in the
_[ActionScript 3.0 Reference for the Adobe Flash Platform](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/display/BitmapData.html#getPixel%28%29)_.
You must call this object's `acquire()` function before calling this method.

**Returns:**

`boolean`  
`true` if the pixel color components are already multiplied by the alpha
component.

#### getLineStride32

    public int getLineStride32()

Specifies the amount of data in each horizontal line of the bitmap. Use this
value with the byte array returned by `getBits()` to parse the image. For
example, the position of the pixel immediately below a pixel located at position
`n` in the byte array is `n + getLineStride32()`. You must call this object's
`acquire()` function before calling this method.

**Returns:**

`int`  
The amount of data for each horizontal line in the image.

**Example:**

The following example moves the position of the byte array containing the pixels
colors to the beginning of the third line in a bitmap:

    Byte[] fillColor = {0xf,0xf,0xf,0xf,0xf,0xf,0xf,0xf};
    FREBitmapData bitmap = FREBitmapData.newBitmapData( 320, 200, true, fillColor );
    int lineStride = bitmap.getLineStride32();
    bitmap.acquire();
    ByteBuffer pixels = bitmap.getBits();
    pixels.position( lineStride * 3 );
    //do something with the image data
    bitmap.release();

#### getBits

    ByteBuffer getBits()

Returns an array of pixel color values. You must call `acquire()` before using
this method and call `release()` when you are done modifying the data. If you
make changes to the pixel data, call `invalidateRect()` to notify the AIR
runtime that the bitmap has changed. Otherwise, the displayed graphics are not
updated.

**Returns:**

`java.nio.ByteBuffer`  
The image data.

**Example:**

    FREBitmapData bitmap = FREBitmapData.newBitmapData( 320, 200, true, fillColor );
    bitmap.acquire();
    ByteBuffer pixels = bitmap.getBits();
    //do something with the image data
    bitmap.release();

#### acquire

    public void acquire()

Acquires a lock on the image so that the data cannot be modified or disposed by
the runtime or application code while you are accessing it. You only need to
acquire a lock for bitmaps passed to the function from the ActionScript side of
the extension.

While you have a lock, you can only access the data returned by the `getBits()`
function. Accessing or attempting to modify the other properties of the
FREBitmapData results in an exception.

#### invalidateRect

    void invalidateRect( int x, int y, int width, int height )

Notifies the runtime that you have changed a region of the image. The screen
display of a bitmap data object is not updated unless you call this method. You
must call this object's `acquire()` function before calling this method.

**Parameters:**

`x`  
The upper-left corner of the rectangle to invalidate.

`y`  
the upper-left corner of the rectangle to invalidate.

`width`  
the width of the rectangle to invalidate.

`height`  
the height of the rectangle to invalidate.

#### release

    public void release()

Releases the lock obtained by `acquire()`. You must release the lock before
accessing any bitmap properties other than the pixel data returned by
`getBits()`.

#### isInvertedY

    public boolean isInvertedY()

Indicates the order in which the rows of image data are stored. If `true`, then
the last row of image data appears first in the buffer returned by the
`getBits()` method. Images on Android are normally stored starting with the
first row of data, so this property is typically `false` on the Android
platform.

Added in AIR 3.1.
