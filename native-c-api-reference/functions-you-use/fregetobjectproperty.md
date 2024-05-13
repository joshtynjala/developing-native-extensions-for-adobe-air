# FREGetObjectProperty()

#### Usage

    FREResult FREGetObjectProperty (
                FREObject                 object,
                const uint8_t*                 propertyName,
                FREObject*                propertyValue,
                FREObject*                thrownException
    );

#### Parameters

object  
An FREObject that represents the ActionScript class object from which to fetch
the value of a property.

propertyName  
A uint8_t array. This array contains a string that is the name of property. Use
UTF-8 encoding for the string and terminate it with the null character.

propertyValue  
A pointer to an FREObject. This method sets this FREObject parameter to
represent an ActionScript object that is the requested property.

thrownException  
A pointer to an FREObject. If calling this method results in the runtime
throwing an ActionScript exception, this FREObject variable represents the
ActionScript Error, or Error subclass, object. If no error occurs, the runtime
sets this FREObject variable to be invalid. That is, `FREGetObjectType()` for
the thrownException FREObject variable returns `FRE_INVALID_OBJECT`. This
pointer can be `NULL` if you do not want to handle exception information.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded and the `propertyValue` parameter is correctly set.

FRE_ACTIONSCRIPT_ERROR  
An ActionScript error occurred. The runtime sets the `thrownException` parameter
to represent the ActionScript Error class or subclass object.

FRE_ILLEGAL_STATE  
The extension context has acquired an ActionScript BitmapData or ByteArray
object. The context cannot call this method until it releases the BitmapData or
ByteArray object.

FRE_INVALID_ARGUMENT  
The `propertyName` or `propertyValue` parameter is `NULL`.

FRE_INVALID_OBJECT  
The FREObject parameter is invalid.

FRE_NO_SUCH_NAME  
The `propertyName` parameter does not match a property of the ActionScript class
object that the `object` parameter represents. Another, less likely, reason for
this return value exists. Specifically, consider the unusual case when an
ActionScript class has two properties with the same name but the names are in
different ActionScript namespaces.

FRE_TYPE_MISMATCH  
The FREObject parameter does not represent an ActionScript class object.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to get the FREObject variable to the data that corresponds to
a public property of an ActionScript class object specified by the `object`
parameter.

More Help topics

[FRESetObjectProperty()](./fresetobjectproperty.md)

[The FREObject type](../../coding-the-native-side-with-c/the-freobject-type.md)
