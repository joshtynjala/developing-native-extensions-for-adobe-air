# FRENewObjectFromUint32()

#### Usage

    FREResult FRENewObjectFromUint32 ( uint32_t value, FREObject* object);

#### Parameters

value  
A uint32_t that is the value for a new ActionScript int instance with a value
greater than or equal to 0.

object  
A pointer to an FREObject that represents an int ActionScript instance.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded and the `object` parameter is correctly set.

FRE_INVALID_ARGUMENT  
The FREObject parameter is `NULL`.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to create an ActionScript int instance with the `value`
parameter. The runtime sets the FREObject variable to correspond to the new
ActionScript int instance.

More Help topics

[FREGetObjectAsUint32()](./fregetobjectasuint32.md)

[The FREObject type](../../coding-the-native-side-with-c/the-freobject-type.md)
