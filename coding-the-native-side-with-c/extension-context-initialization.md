# Extension context initialization

To use the native C methods, the ActionScript side of your extension first calls
the static method `ExtensionContext.createExtensionContext()`. Calling
`createExtensionContext()` causes the runtime to do the following:

- Create an ExtensionContext instance.

- Create internal data it uses to track the extension context.

- Call the extension context initialization function.

The extension context initialization function initializes the native
implementation for the new extension context. Define your extension context
initializer function with the signature of
[FREContextInitializer()](../native-c-api-reference/functions-you-implement/frecontextinitializer.md).

For example, the Vibration example uses the following function:

    void ContextInitializer(void* extData, const uint8_t* ctxType, FREContext ctx,
                        uint32_t* numFunctionsToSet,
                        const FRENamedFunction** functionsToSet) {

        *numFunctionsToSet = 2;

        FRENamedFunction* func = (FRENamedFunction*)malloc(sizeof(FRENamedFunction)*2);
        func[0].name = (const uint8_t*)"isSupported";
        func[0].functionData = NULL;
        func[0].function = &IsSupported;

        func[1].name = (const uint8_t*)"vibrateDevice";
        func[1].functionData = NULL;
        func[1].function = &VibrateDevice;

        *functionsToSet = func;
    }

A context initialization function receives the following input parameters:

- The extension data that the extension initialization function had created. See
  [Extension initialization](./extension-initialization.md).

- The context type. The ActionScript method
  `ExtensionContext.createExtensionContext()` is passed a parameter that
  specifies the context type. The runtime passes this string value to the
  context initialization function. The function then uses the context type to
  choose the set of methods in the native implementation that the ActionScript
  side can call. Each context type typically corresponds to a different set of
  methods. See
  [The context type](../coding-the-actionscript-side/create-an-extensioncontext-instance.md#the-context-type).

  The value of the context type is any string agreed to between the ActionScript
  side and the native side.

  If your extension has only one set of methods in the native implementation,
  pass null or an empty string in `ExtensionContext.createExtensionContext()`.
  Then ignore the context type parameter in the extension context initializer.

- A FREContext value. The runtime creates internal data when it creates an
  extension context. It associates the internal data with the ExtensionContext
  class instance on the ActionScript side.

  When your native implementation dispatches an event the ActionScript side, it
  specifies this FREContext value. The runtime uses the FREContext value to
  dispatch the event to the corresponding ExtensionContext instance. See
  [FREDispatchStatusEventAsync()](../native-c-api-reference/functions-you-use/fredispatchstatuseventasync.md).

  Also, native functions can use this value to access and set the
  context-specific native data and context-specific ActionScript data.

The extension context initialization function sets the following output
parameters:

- An array of native functions. The ActionScript side can call each of these
  functions by using the ExtensionContext instance's `call()` method.

  The type of each array element is `FRENamedFunction`. This structure includes
  a string which is the name the ActionScript side uses to call the function.
  The structure also includes a pointer to the C function you write. The runtime
  associates the name with the C function. Although the name string does not
  have to match the actual function name, typically you use the same name.

- The number of functions in the array of native functions.

A sequence diagram showing the AIR runtime calling the `FREContextInitializer()`
function is in [Extension initialization](./extension-initialization.md).

More Help topics

[Vibration native extension example](https://web.archive.org/web/20150227130512/http://www.adobe.com/devnet/air/native-extensions-for-air/extensions/vibration.html)
