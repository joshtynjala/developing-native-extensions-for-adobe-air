# Accessing ActionScript objects

An instance of the
[FREObject](../android-java-api-reference/classes/freobject.md) class represents
an ActionScript class object or primitive type. Use FREObject instances in your
Java implementation to work with ActionScript data. A primary use of FREObjects
is for Java function parameters and return values.

The FREObject class provides functions for accessing the associated ActionScript
class object or primitive value. The Java APIs that you use depend on the type
of the ActionScript object. These types can be the following:

- An ActionScript primitive data type

- An ActionScript class object

- An ActionScript String object

- An ActionScript Array or Vector class object

- An ActionScript ByteArray class object

- An ActionScript BitmapData class object

Important: You can only access an FREObject from the same thread as the one in
which the "owning" FREFunction function is running. In addition, if you have
called the `acquire()` method of any FREByteArray or FREBitmapData object, you
cannot access the ActionScript methods of any object until you call the
`release()` method for the original FREByteArray or FREBitmapData object. When
any object is "acquired," calling the `getProperty()`, `setProperty()`, or
`callMethod()` of that or any other FREObject throws an IllegalStateException.

## FREObject validity

If you attempt to use an invalid
[FREObject](../android-java-api-reference/classes/freobject.md) in a Java API
call, the Java API throws an exception.

Any FREObject instance is valid only until the first FREFunction function on the
call stack returns. The first FREFunction function on the call stack function is
the one that the runtime calls due to the ActionScript side calling the
ExtensionContext instance's `call()` method. FREObjects are also only valid in
the thread used by the runtime to call the first FREFunction.

> **Note:** An FREFunction function can indirectly call another FREFunction
> function. For example, `FREFunctionA()` can call a method of an ActionScript
> object. That method then can call `FREFunctionB()`.

Therefore, when using an FREObject, consider the following:

- Any FREObject passed to an FREFunction instance is valid only until the first
  FREFunction on the call stack returns.

- Any FREObject that any Java function creates is valid only until the first
  FREFunction on the call stack returns.

- You cannot use an FREObject in another thread. Only use the FREObject in the
  same thread as the Java function that received or created the object.

- You cannot save an FREObject reference, for example in global data, between
  calls to FREFunction functions. Because the object becomes invalid when the
  first FREFunction function on the call stack returns, the saved reference is
  useless. However, you can use the `setActionScriptData()` method of the
  FREContext class to save data between function invocations.

- After an FREObject becomes invalid, the corresponding ActionScript object can
  still exist. For example, if an FREObject is a return value of an FREFunction
  function, its corresponding ActionScript object is still referenced. However,
  once the ActionScript side deletes its references, the runtime disposes of the
  ActionScript object.

- You cannot share FREObjects between extensions.

  > **Note:** You can share FREObjects between extension contexts of the same
  > extension. However, in this, as in any case, the FREObject still becomes
  > invalid when the first FREFunction function on the call stack returns to the
  > runtime.
