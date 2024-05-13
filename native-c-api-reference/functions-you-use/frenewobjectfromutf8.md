# FRENewObjectFromUTF8()

#### Usage

    FREResult FRENewObjectFromUTF8(uint32_t length, const uint8_t* value, FREObject* object);

#### Parameters

length  
A uint32_t that is the length of the string in the `value` parameter, including
the null terminator.

value  
An array of uint8_t elements. The array is the value for the new ActionScript
String object. The FREObject variable represents a String ActionScript variable.
Use UTF-8 encoding for the string and terminate it with the null character.

object  
A pointer to an FREObject that points to the data that represents a String
ActionScript object.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded and the `object` parameter is correctly set.

FRE_INVALID_ARGUMENT  
The `object` or `value` parameter is `NULL`.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to create an ActionScript String object with the string value
specified in `value`. This method sets the FREObject output parameter `object`
to correspond to the new ActionScript String instance.

More Help topics

[FREGetObjectAsUTF8()](./fregetobjectasutf8.md)

[The FREObject type](../../coding-the-native-side-with-c/the-freobject-type.md)
