# FREFinalizer()

#### Signature

    typedef void (*FREFinalizer)(
        void*     extData,
    );

#### Parameters

extData  
A pointer to the extension data of the extension.

#### Returns

Nothing.

#### Description

The runtime calls this function when it unloads an extension. However, the
runtime does not guarantee that it will unload the extension or call
`FREFinalizer()`.

Implement this function to clean up extension resources.

More Help topics

[FREInitializer()](./freinitializer.md)

[Extension finalization](../../coding-the-native-side-with-c/extension-finalization.md)
