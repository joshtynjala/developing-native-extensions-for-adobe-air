# FRECallObjectMethod()

#### Usage

    FREResult FRECallObjectMethod(
            FREObject                 object,
            const uint8_t*                methodName,
            uint32_t                argc,
            FREObject                argv[],
            FREObject*                result,
            FREObject*                thrownException
    );

#### Parameters

object  
An FREObject that represents the ActionScript class object on which a method is
being called.

methodName  
A uint8_t array. This array is a string that is the name of the method being
called. Use UTF-8 encoding for the string and terminate it with the null
character.

argc  
A uint32_t. The value is the number of parameters passed to the method. This
parameter is the length of the `argv` array parameter. The value can be 0 when
the method to call takes no parameters.

argv\[\]  
An FREObject array. Each FREObject element corresponds to the ActionScript class
or primitive type passed as a parameter to the method being called. The value
can be `NULL` when the method to call takes no parameters.

result  
A pointer to an FREObject. This FREObject variable is to receive the return
value of the method being called. The FREObject variable represents the
ActionScript class or primitive type that the method being called returns.

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
The function succeeded. The ActionScript method returned without throwing an
exception.

FRE_ACTIONSCRIPT_ERROR  
An ActionScript error occurred. The runtime sets the `thrownException` parameter
to represent the ActionScript Error class or subclass object.

FRE_ILLEGAL_STATE  
The extension context has acquired an ActionScript BitmapData or ByteArray
object. The context cannot call this method until it releases the BitmapData or
ByteArray object.

FRE_INVALID_ARGUMENT  
The `method` or `result` parameter is `NULL`, or `argc` is greater than 0 but
`argv` is `NULL`.

FRE_INVALID_OBJECT  
The FREObject parameter or an `argv` FREObject element is invalid.

FRE_NO_SUCH_NAME  
The `methodName` parameter does not match a method of the ActionScript class
object that the `object` parameter represents. Another, less likely, reason for
this return value exists. Specifically, consider the unusual case when an
ActionScript class has two methods with the same name but the names are in
different ActionScript namespaces.

FRE_TYPE_MISMATCH  
The FREObject parameter does not represent an ActionScript class object.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to call a method of an ActionScript class object.

More Help topics

[The FREObject type](../../coding-the-native-side-with-c/the-freobject-type.md)
