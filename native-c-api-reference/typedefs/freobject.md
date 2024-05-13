# FREObject

    typedef void* FREObject;

When you access an ActionScript class object or primitive data type variable
from your native C implementation, you use an FREObject variable. The runtime
associates an FREObject variable with the corresponding ActionScript object.

FREObject variables are used in native functions you implement with the
signature [FREFunction()](../functions-you-implement/frefunction.md). The native
functions:

- Receive FREObject variables as parameters.

- Return an FREObject variable.

FREObject variables are also used when you use native extensions C API functions
to:

- Create an ActionScript class object or ActionScript primitive data type.

- Get the value of an ActionScript class object or ActionScript primitive data
  type.

- Create an ActionScript String object.

- Get the value of an ActionScript String object.

- Get or set a property of an ActionScript object.

- Call a method of an ActionScript object.

- Access the bits of an ActionScript BitmapData object.

- Access the bytes of an ActionScript ByteArray object.

- Get or set the length of an ActionScript Array or Vector object.

- Get or set an element of an ActionScript Array or Vector object.

- Get an ActionScript Error object when the runtime throws an exception in a
  native extension C API function call.

- Set or get an ActionScript object in the ActionScript context data.
