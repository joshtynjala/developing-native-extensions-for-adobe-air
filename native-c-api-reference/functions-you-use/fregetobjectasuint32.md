# FREGetObjectAsUint32()

#### Usage

    FREResult FREGetObjectAsUint32 ( FREObject object, uint32_t *value );

#### Parameters

object  
An FREObject.

value  
A pointer to a uint32_t. The function sets this value to correspond to the value
of the Boolean or int ActionScript variable that the FREObject variable
represents.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded and the `value` parameter is correctly set.

FRE_TYPE_MISMATCH  
The FREObject parameter does not contain a Boolean or int ActionScript value. An
int ActionScript value that is negative also results in this return value.

FRE_INVALID_OBJECT  
The FREObject parameter is invalid.

FRE_INVALID_ARGUMENT  
The value parameter is `NULL`.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to set the value of a C uint32_t variable to the value of an
ActionScript Boolean or int variable.

More Help topics

[FRENewObjectFromUint32()](./frenewobjectfromuint32.md)

[The FREObject type](../../coding-the-native-side-with-c/the-freobject-type.md)
