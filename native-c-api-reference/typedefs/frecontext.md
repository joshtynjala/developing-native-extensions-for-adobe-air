# FREContext

    typedef void* FREContext;

The ActionScript side creates an extension context by calling
`ExtensionContext.createExtensionContext()`. For each extension context, the AIR
runtime creates a corresponding FREContext variable.

The runtime passes the FREContext variable to each of the following functions in
the native implementation:

- The context initialization function,
  [FREContextInitializer()](../functions-you-implement/frecontextinitializer.md).

- The context finalizer function,
  [FREContextFinalizer()](../functions-you-implement/frecontextfinalizer.md).

- Each extension function,
  [FREFunction()](../functions-you-implement/frefunction.md).

Use this FREContext variable when:

- You dispatch an event to the ActionScript ExtensionContext instance. See
  [FREDispatchStatusEventAsync()](../functions-you-use/fredispatchstatuseventasync.md).

- You get or set native context data. See
  [FREGetContextNativeData()](../functions-you-use/fregetcontextnativedata.md)
  and
  [FRESetContextNativeData()](../functions-you-use/fresetcontextnativedata.md).

- You get or set ActionScript context data. See
  [FREGetContextActionScriptData()](../functions-you-use/fregetcontextactionscriptdata.md)
  and
  [FRESetContextActionScriptData()](../functions-you-use/fresetcontextactionscriptdata.md).
