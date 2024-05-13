# FREGetObjectAsUTF8()

#### Usage

    FREResult FREGetObjectAsUTF8(FREObject object, uint32_t* length, const uint8_t** value);

#### Parameters

object  
An FREObject.

length  
A pointer to a uint32_t. The value of `length` is the number of bytes in the
`value` array. The length includes the null terminator. The length corresponds
to the length of the String ActionScript variable that the FREObject variable
represents.

value  
A pointer to a uint8_t array. The function fills the array with the characters
of the String ActionScript variable that the FREObject variable represents. The
string uses UTF-8 encoding terminates with the null character.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded and the `value` and `length` parameters are correctly
set.

FRE_TYPE_MISMATCH  
The FREObject parameter does not contain a String ActionScript value.

FRE_INVALID_OBJECT  
The FREObject parameter is invalid.

FRE_INVALID_ARGUMENT  
The `value` or `length` parameter is `NULL`.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to set the value of a uint8_t array to the string value of an
ActionScript String object.

Consider the following regarding the string returned in the `value` parameter:

- You cannot change the string.

- The string is valid only until the native extension function that the runtime
  called returns.

- The string becomes invalid if you call any other C API function.

Therefore, to manipulate or access the string later, copy it immediately into
your own array.

More Help topics

[FRENewObjectFromUTF8()](./frenewobjectfromutf8.md)

[The FREObject type](../../coding-the-native-side-with-c/the-freobject-type.md)
