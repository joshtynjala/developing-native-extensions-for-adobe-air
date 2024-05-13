# FRENewObjectFromDouble()

#### Usage

    FREResult FRENewObjectFromDouble ( double value, FREObject* object);

#### Parameters

value  
A double that is the value for a new ActionScript Number instance.

object  
A pointer to an FREObject that points to the data that represents a Number
ActionScript variable.

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

Call this function to create an ActionScript Number instance with the `value`
parameter. The runtime sets the FREObject variable to the data corresponding to
the new ActionScript instance.

More Help topics

[FREGetObjectAsDouble()](./fregetobjectasdouble.md)

[The FREObject type](../../coding-the-native-side-with-c/the-freobject-type.md)
