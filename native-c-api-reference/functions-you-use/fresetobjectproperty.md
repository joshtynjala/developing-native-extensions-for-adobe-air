# FRESetObjectProperty()

#### Usage

    FREResult FRESetObjectProperty (
                FREObject                 object,
                const uint8_t*                 propertyName,
                FREObject                propertyValue,
                FREObject*                thrownException
    );

#### Parameters

object  
An FREObject that represents the ActionScript class object for which a property
is to be set.

propertyName  
A uint8_t array. This array contains a string that is the name of property to
set. Use UTF-8 encoding for the string and terminate it with the null character.

propertyValue  
An FREObject that represents the value to set the property to.

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
The function succeeded and the ActionScript class object's property is correctly
set.

FRE_ACTIONSCRIPT_ERROR  
An ActionScript error occurred. The runtime sets the `thrownException` parameter
to represent the ActionScript Error class or subclass object.

FRE_ILLEGAL_STATE  
The extension context has acquired an ActionScript BitmapData or ByteArray
object. The context cannot call this method until it releases the BitmapData or
ByteArray object.

FRE_INVALID_ARGUMENT  
The `propertyName` parameter is `NULL`.

FRE_INVALID_OBJECT  
The `object` or `propertyValue` parameter is an invalid FREObject variable.

FRE_NO_SUCH_NAME  
The `propertyName` parameter does not match a property of the ActionScript class
object that the `object` parameter represents. Another, less likely, reason for
this return value exists. Specifically, consider the unusual case when an
ActionScript class has two properties with the same name but the names are in
different ActionScript namespaces.

FRE_READ_ONLY  
The property to set is a read-only property.

FRE_TYPE_MISMATCH  
The FREObject `object` parameter does not represent an ActionScript class
object.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to set the value of a public property of the ActionScript
class object that an FREObject variable represents. Pass the name of the
property to set in the `propertyName` parameter. Pass the new property value in
the `propertyValue` parameter.

More Help topics

[FREGetObjectProperty()](./fregetobjectproperty.md)

[The FREObject type](../../coding-the-native-side-with-c/the-freobject-type.md)
