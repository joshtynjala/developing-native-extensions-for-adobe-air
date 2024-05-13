# Dispose of an ExtensionContext instance

The ActionScript extension class can dispose of the ExtensionContext instance by
calling the ExtensionContext method `dispose()`. This method notifies the native
implementation to clean up resources that the instance uses. For example, the
TVChannelController class can add a method for cleaning up:

    public function dispose(): void {
        extContext.dispose();
        // Clean up other resources that the TVChannelController instance uses.
    }

Your ActionScript extension class does not have to explicitly call the
ExtensionContext instance's `dispose()` method. In this case, the runtime calls
it when the runtime garbage collector disposes of the ExtensionContext instance.
A best practice, however, is to explicitly call `dispose()`. An explicit call to
`dispose()` typically cleans up resources much sooner than waiting for the
garbage collector.

Whether called explicitly or by the garbage collector, the ExtensionContext
`dispose()` method results in a call to the native implementation's context
finalizer. For more information, see
[Extension context finalization](../coding-the-native-side-with-c/extension-context-finalization.md).
