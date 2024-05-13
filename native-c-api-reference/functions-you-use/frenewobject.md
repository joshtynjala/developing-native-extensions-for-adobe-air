# FRENewObject()

#### Usage

    FREResult FRENewObject(
            const uint8_t*                className,
            uint32_t                argc,
            FREObject                argv[],
            FREObject*                object,
            FREObject*                thrownException
    );

#### Parameters

className  
A uint8_t array. A string that is the name of the ActionScript class to create
an object of. Use UTF-8 encoding for the string and terminate it with the null
character.

argc  
A uint32_t. The number of parameters passed to the constructor of the
ActionScript class. This parameter is the length of the `argv` array parameter.
The value can be 0 when the constructor takes no parameters.

argv\[\]  
An FREObject array. Each FREObject element corresponds to the ActionScript class
or primitive type passed as a parameter to the constructor. The value can be
`NULL` when the constructor takes no parameters.

object  
A pointer to an FREObject. When this method returns successfully, this FREObject
variable represents the new ActionScript class object.

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
The function succeeded. The `object` parameter represents the new ActionScript
class object.

FRE_ACTIONSCRIPT_ERROR  
An ActionScript error occurred. The runtime sets the `thrownException` parameter
to represent the ActionScript Error class or subclass object.

FRE_ILLEGAL_STATE  
The extension context has acquired an ActionScript BitmapData or ByteArray
object. The context cannot call this method until it releases the BitmapData or
ByteArray object.

FRE_INVALID_ARGUMENT  
The `className` or `object` parameter is `NULL`, or `argc` is greater than 0 but
`argv` is `NULL` or empty.

FRE_NO_SUCH_NAME  
The `className` parameter does not match an ActionScript class name.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to create an object of an ActionScript class. The constructor
that the runtime calls depends on the parameters you pass in the `argv` array.

More Help topics

[The FREObject type](../../coding-the-native-side-with-c/the-freobject-type.md)
