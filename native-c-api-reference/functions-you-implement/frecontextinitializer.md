# FREContextInitializer()

#### Signature

    typedef void (*FREContextInitializer)(
        void*                        extData,
        const uint8_t*           ctxType,
        FREContext               ctx,
        uint32_t*                numFunctionsToSet,
        const FRENamedFunction** functionsToSet
    );

#### Parameters

extData  
A pointer to the extension data of the native extension. The function
[FREInitializer()](../functions-you-implement/freinitializer.md) created the
extension data.

ctxType  
A string identifying the type of the context. You define this string as required
by your extension. The context type can indicate any agreed-to meaning between
the ActionScript side and native side of the extension. If your extension has no
use for context types, this value can be `Null`. This value is a UTF-8 encoded
string, terminated with the null character.

ctx  
An FREContext variable. The runtime creates this value and passes it to
`FREContextInitializer()`. See [FREContext](../typedefs/frecontext.md).

numFunctionsToSet  
A pointer to a `unint32_t`. Set `numFunctionsToSet` to a `unint32_t` variable
containing the number of functions in the `functionsToSet` parameter.

functionsToSet  
A pointer to an array of FRNamedFunction elements. Each element contains a
pointer to a native function, and the string the ActionScript side uses in the
ExtensionContext instance's `call()` method. See
[FRENamedFunction](../structure-typedefs/frenamedfunction.md).

#### Returns

Nothing.

#### Description

The runtime calls this method when the ActionScript side calls
`ExtensionContext.createExtensionContext()`. Implement this method to do the
following:

- Initialize your extension context. The initializations can depend on the
  context type passed in the `ctxType` parameter.

- Save the value of the `ctx` parameter so it is available to calls the native
  implementation makes to `FREDispatchStatusEventAsync()`.

- Use the `ctx` parameter to initialize context-specific data. This data
  includes context-specific native data and context-specific ActionScript data.

- Set up an array of FRENamedFunction objects. Return a pointer to the array in
  the `functionsToSet` parameter. Return a pointer to the number of array
  elements in the `numFunctionsToSet` parameter.

The behavior your FREContextInitializer() method can depend on the `ctxType`
parameter. The ActionScript side can pass a context type to
`ExtensionContext.createExtensionContext()`. Then, the runtime passes the value
to `FREContextInitializer().` This function typically uses the context type to
choose the set of methods in the native implementation that the ActionScript
side can call. Each context type corresponds to a different set of methods.

More Help topics

[The context type](../../coding-the-actionscript-side/create-an-extensioncontext-instance.md#the-context-type)

[Extension context initialization](../../coding-the-native-side-with-c/extension-context-initialization.md)
