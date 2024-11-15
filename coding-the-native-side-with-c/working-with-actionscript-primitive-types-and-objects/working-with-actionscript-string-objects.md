# Working with ActionScript String objects

In your native functions, an input parameter can correspond to an ActionScript
String class object. All native function parameters are of type FREObject.
Therefore, to work with an ActionScript String parameter, you get the
ActionScript String value of the FREObject parameter. You store the value in a
corresponding C string variable. Use the C API function
[FREGetObjectAsUTF8()](../../native-c-api-reference/functions-you-use/fregetobjectasutf8.md):

    FREResult FREGetObjectAsUTF8(
            FREObject       object,
            uint32_t*       length,
            const uint8_t** value
    );

After calling `FREGetObjectAsUTF8()`, the ActionScript String value is in the
`value` parameter, and the `length` parameter tells the length of the value
string in bytes.

If an output parameter or return value corresponds to an ActionScript String
class object, you create the ActionScript String object using a C API. You
provide a pointer to a FREObject variable and the string value and length in
bytes in C string variables. The runtime creates the ActionScript String object
and sets the FREObject variable to correspond to it. Use the C API function
[FRENewObjectFromUTF8()](../../native-c-api-reference/functions-you-use/frenewobjectfromutf8.md):

    FREResult FRENewObjectFromUTF8(
            uint32_t        length,
            const uint8_t*  value,
            FREObject*      object
    );

The `value` parameter strings must use UTF- 8 encoding and include the null
terminator.

> **Note:** All string parameters to any C API function use UTF-8 encoding and
> include the null terminator.
