# FREGetObjectType()

#### Usage

    FREResult FREGetObjectType( FREObject object, FREObjectType *objectType );

#### Parameters

object  
An FREObject variable.

objectType  
A pointer to an FREObjectType variable. `FREGetObjectType()` sets this variable
to one of the FREObjectType enumeration values.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded and the `objectType` parameter is correctly set.

FRE_INVALID_ARGUMENT  
The `objectType` parameter is `NULL`.

FRE_INVALID_OBJECT  
The FREObject parameter is invalid.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to get the FREObjectType enumeration value that best
describes an FREObject variable's corresponding ActionScript class object or
primitive type.

More Help topics

[FREObjectType](../enumerations/freobjecttype.md)

[The FREObject type](../../coding-the-native-side-with-c/the-freobject-type.md)
