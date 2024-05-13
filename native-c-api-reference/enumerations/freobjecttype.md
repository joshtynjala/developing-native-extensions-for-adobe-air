# FREObjectType

An FREObject variable corresponds to an ActionScript class object or primitive
type. The FREObjectType enumeration defines values for these ActionScript class
types and primitive types. The C API function
[FREGetObjectType()](../functions-you-use/fregetobjecttype.md) returns an
FREObjectType enumeration value that best describes an FREObject variable's
corresponding ActionScript class object or primitive type.

    enum FREObjectType {
        FRE_TYPE_OBJECT                          = 0,
        FRE_TYPE_NUMBER                          = 1,
        FRE_TYPE_STRING                          = 2,
        FRE_TYPE_BYTEARRAY                       = 3,
        FRE_TYPE_ARRAY                           = 4,
        FRE_TYPE_VECTOR                          = 5,
        FRE_TYPE_BITMAPDATA                      = 6,
        FRE_TYPE_BOOLEAN                         = 7,
        FRE_TYPE_NULL                            = 8,
        FREObjectType_ENUMPADDING                = 0xfffff
    };

The enumeration values have the following meanings:

FRE_TYPE_OBJECT  
The FREObject variable corresponds to an ActionScript class object that is not a
String object, ByteArray object, Array object, Vector object, or BitmapData
object.

FRE_TYPE_NUMBER  
The FREObject variable corresponds to an ActionScript Number variable.

FRE_TYPE_STRING  
The FREObject variable corresponds to an ActionScript String object.

FRE_TYPE_BYTEARRAY  
The FREObject variable corresponds to an ActionScript ByteArray object.

FRE_TYPE_ARRAY  
The FREObject variable corresponds to an ActionScript Array object.

FRE_TYPE_VECTOR  
The FREObject variable corresponds to an ActionScript Vector object.

FRE_TYPE_BITMAPDATA  
The FREObject variable corresponds to an ActionScript BitmapData object.

FRE_TYPE_BOOLEAN  
The FREObject variable corresponds to an ActionScript Boolean variable.

FRE_TYPE_NULL  
The FREObject variable corresponds to the ActionScript value `Null` or
`undefined`.

FREObjectType_ENUMPADDING  
This final enumeration value is to guarantee that the size of an enumeration
value is always 4 bytes.

More Help topics

[The FREObject type](../../coding-the-native-side-with-c/the-freobject-type.md)
