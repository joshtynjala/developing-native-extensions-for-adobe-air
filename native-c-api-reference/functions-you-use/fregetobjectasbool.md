# FREGetObjectAsBool()

#### Usage

    FREResult FREGetObjectAsBool  ( FREObject object, unint32_t *value );

#### Parameters

object  
An FREObject.

value  
A pointer to a uint32_t. The function sets this value to correspond to the value
of the Boolean ActionScript variable that the FREObject variable represents. A
non-zero value corresponds to `true`. A zero value corresponds to `false`.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded and the `value` parameter is correctly set.

FRE_TYPE_MISMATCH  
The FREObject parameter does not contain a Boolean ActionScript value.

FRE_INVALID_OBJECT  
The FREObject parameter is invalid.

FRE_INVALID_ARGUMENT  
The value parameter is `NULL`.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to set the value of a C uint32_t variable to the value of an
ActionScript Boolean variable.

More Help topics

[FRENewObjectFromBool()](./frenewobjectfrombool.md)

[The FREObject type](../../coding-the-native-side-with-c/the-freobject-type.md)
