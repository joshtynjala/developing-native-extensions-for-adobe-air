# FREGetObjectAsInt32()

#### Usage

    FREResult FREGetObjectAsInt32 ( FREObject object, int32_t *value );

#### Parameters

object  
An FREObject.

value  
A pointer to an int32_t. The function sets this value to correspond to the value
of the Boolean or int ActionScript variable that the FREObject variable
represents.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded and the `value` parameter is correctly set.

FRE_TYPE_MISMATCH  
The FREObject parameter does not contain a Boolean or int ActionScript value.

FRE_INVALID_OBJECT  
The FREObject parameter is invalid.

FRE_INVALID_ARGUMENT  
The value parameter is `NULL`.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to set the value of a C int32_t variable to the value of an
int or Boolean ActionScript variable.

More Help topics

[FRENewObjectFromInt32()](./frenewobjectfromint32.md)

[The FREObject type](../../coding-the-native-side-with-c/the-freobject-type.md)
