# Working with ActionScript primitive types

In your native functions, an input parameter can correspond to a primitive
ActionScript type. All native function parameters are of type FREObject.
Therefore, to work with an ActionScript primitive type input parameter, you get
the ActionScript value of the FREObject parameter. You store the value in a
corresponding primitive C data type variable. Use the following C API functions:

- [FREGetObjectAsInt32()](../../native-c-api-reference/functions-you-use/fregetobjectasint32.md)

      FREResult FREGetObjectAsInt32(FREObject object, int32_t *value);

- [FREGetObjectAsUint32()](../../native-c-api-reference/functions-you-use/fregetobjectasuint32.md)

      FREResult FREGetObjectAsUint32(FREObject object, uint32_t *value);

- [FREGetObjectAsDouble()](../../native-c-api-reference/functions-you-use/fregetobjectasdouble.md)

      FREResult FREGetObjectAsDouble(FREObject object, double *value);

- [FREGetObjectAsBool()](../../native-c-api-reference/functions-you-use/fregetobjectasbool.md),

      FREResult FREGetObjectAsBool  (FREObject object, bool *value);

If an output parameter or return value corresponds to a primitive ActionScript
type, you create the ActionScript primitive using a C API function. You provide
a pointer to an FREObject variable and the value of the primitive in a C data
variable. The runtime creates the ActionScript primitive and sets the FREObject
variable to correspond to it. Use the following C API functions:

- [FRENewObjectFromInt32()](../../native-c-api-reference/functions-you-use/frenewobjectfromint32.md)

      FREResult FRENewObjectFromInt32(int32_t value, FREObject *object);

- [FRENewObjectFromUint32()](../../native-c-api-reference/functions-you-use/frenewobjectfromuint32.md)

      FREResult FRENewObjectFromUint32(uint32_t value, FREObject *object);

- [FRENewObjectFromDouble()](../../native-c-api-reference/functions-you-use/frenewobjectfromdouble.md)

      FREResult FRENewObjectFromDouble(double value, FREObject *object);

- [FRENewObjectFromBool()](../../native-c-api-reference/functions-you-use/frenewobjectfrombool.md),

      FREResult FRENewObjectFromBool  (bool value, FREObject *object);
