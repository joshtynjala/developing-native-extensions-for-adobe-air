# Working with ActionScript Class objects

In your native functions, an input parameter can correspond to an ActionScript
class object. Since all native function parameters are of type FREObject, the C
APIs provide functions for manipulating class objects using an FREObject
variable.

Use the following C API functions to get and set a property of the ActionScript
class object:

- [FREGetObjectProperty()](../../native-c-api-reference/functions-you-use/fregetobjectproperty.md)

      FREResult FREGetObjectProperty(
              FREObject     object,
              const uint8_t*                propertyName,
              FREObject*                       propertyValue,
                 FREObject*                   thrownException
      );

- [FRESetObjectProperty()](../../native-c-api-reference/functions-you-use/fresetobjectproperty.md)

      REResult FRESetObjectProperty(
              FREObject       object,
              const uint8_t*  propertyName,
              FREObject       propertyValue,
              FREObject*      thrownException
      );

Use the following C API to call a method of an ActionScript class object:

[FRECallObjectMethod()](../../native-c-api-reference/functions-you-use/frecallobjectmethod.md)

    FREResult FRECallObjectMethod(
            FREObject                object,
            const uint8_t*                methodName,
            uint32_t                argc,
            FREObject                argv[],
            FREObject*                result,
            FREObject*                thrownException
    );

If an output parameter or return value corresponds to an ActionScript class
object, you create the ActionScript object using a C API. You provide a pointer
to an FREObject variable plus FREObject variables to correspond to parameters to
the ActionScript class constructor. The runtime creates the ActionScript class
object and sets the FREObject variable to correspond to it. Use the following C
API function:

[FRENewObject()](../../native-c-api-reference/functions-you-use/frenewobject.md)

    FREResult FRENewObject(
        const uint8_t* className,
        uint32_t       argc,
        FREObject      argv[],
        FREObject*     object,
        FREObject*     thrownException
    );

> **Note:** These general ActionScript object manipulation functions apply to
> all ActionScript class objects. However, the ActionScript classes Array,
> Vector, ByteArray, and BitmapData are special cases because they each involve
> large amounts of data. Therefore, the C API provides additional specific
> functions for manipulating objects of these special cases.
