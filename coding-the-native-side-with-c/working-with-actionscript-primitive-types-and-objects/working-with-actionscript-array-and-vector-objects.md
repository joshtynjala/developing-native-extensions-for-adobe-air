# Working with ActionScript Array and Vector objects

Use the ActionScript Vector and Array classes to efficiently pass arrays between
the ActionScript side and native side of your extension. In your native
functions, an input parameter, output parameter, or return value can correspond
to an ActionScript Array or Vector class object.

As with other ActionScript class objects, an FREObject variable is the native
side representation of an ActionScript Array or Vector object. The C APIs
provide functions for manipulating an Array or Vector class object using an
FREObject variable.

Use the following C API functions to get and set the length of an Array or
Vector object:

- [FREGetArrayLength()](../../native-c-api-reference/functions-you-use/fregetarraylength.md)

      FREResult FREGetArrayLength(
              FREObject  arrayOrVector,
              uint32_t*  length
      );

- [FRESetArrayLength()](../../native-c-api-reference/functions-you-use/fresetarraylength.md)

      FREResult FRESetArrayLength(
              FREObject  arrayOrVector,
              uint32_t   length
      );

Use the following C API functions to get and set an element of an Array or
Vector object:

- [FREGetArrayElementAt()](../../native-c-api-reference/functions-you-use/fregetarrayelementat.md)

      FREResult FREGetArrayElementAt(
              FREObject  arrayOrVector,
              uint32_t   index,
              FREObject* value
      );

- [FRESetArrayElementAt()](../../native-c-api-reference/functions-you-use/fresetarrayelementat.md)

      FREResult FRESetArrayElementAt(
          FREObject  arrayOrVector,
          uint32_t   index,
          FREObject  value
      );
