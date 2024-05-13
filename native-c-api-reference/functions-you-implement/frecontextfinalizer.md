# FREContextFinalizer()

#### Signature

    typedef void (*FREContextFinalizer)(
        FREContext     ctx,
    );

#### Parameters

ctx  
The FREContext variable that represents this extension context. See
[FREContext](../typedefs/frecontext.md).

#### Returns

Nothing.

#### Description

The runtime calls this function when it disposes of the ExtensionContext
instance for this extension context. The following situations cause the runtime
to dispose of the instance:

- The ActionScript side calls the `dispose()` method of the ExtensionContext
  instance.

- The runtime's garbage collector detects no references to the ExtensionContext
  instance.

- The AIR application is shutting down.

Implement this function to clean up resources specific to this context of the
extension. Use the `ctx` parameter to get and then clean up resources associated
with native context data and ActionScript context data. See
[Context-specfic data](../../coding-the-native-side-with-c/context-specific-data.md).

After the runtime calls this function, it calls no other functions of this
extension context.

More Help topics

[Extension context initialization](../../coding-the-native-side-with-c/extension-context-initialization.md)

[Extension context finalization](../../coding-the-native-side-with-c/extension-context-finalization.md)
