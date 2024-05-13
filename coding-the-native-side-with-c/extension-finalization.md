# Extension finalization

The C API provides an extension finalization function for the runtime to call
when it unloads the extension. However, the runtime does not always unload an
extension. Therefore, the runtime does not always call the extension
finalization function.

Define your extension finalization function with the signature of
[FREFinalizer()](../native-c-api-reference/functions-you-implement/frefinalizer.md).
This method has one input parameter: the extension data you created in your
extension initialization function. Clean up any data and resources associated
with this extension.

For application-bundled extensions, your implementation of `FREFinalizer()` can
have any name. Specify the name of the finalization function in the extension
descriptor file. See
[Native extension descriptor files](../native-extension-descriptor-files.md).

For device-bundled applications, how to specify the extension finalization
function is device-dependent.
