# Create an ExtensionContext instance

To begin working with the native implementation, the ActionScript extension
class uses the ExtensionContext static method `createExtensionContext()`. This
method returns a new instance of the ExtensionContext class.

    package com.example {
        public class TVChannelController extends EventDispatcher {

            private var extContext:ExtensionContext;

            public function TVChannelController() {
                extContext = ExtensionContext.createExtensionContext(
                                "com.example.TVControllerExtension", "channel");
            }
            .
            .
            .
        }
    }

In this example, the constructor calls `createExtensionContext()`. Although your
extension classes can call `createExtensionContext()` in any method, typically a
constructor or other initialization method calls it. Save the returned
ExtensionContext instance in a data member of the class.

> Note: Calling `createExtensionContext()` as part of a static data member's
> definition is not recommended. Doing so means that the runtime creates the
> extension context earlier than the application needs it. If the application's
> execution path does not eventually use the extension, creating the context
> wastes device resources.

The method `createExtensionContext()` takes two parameters: an extension ID and
a context type.

## The extension ID

The method `createExtensionContext()` takes a String parameter that is the
identifier, or name, of the extension. This name is the same name you use in the
extension descriptor file in the `id` element. (You create the extension
descriptor file when you package your extension). The application developers
also use this name in the `extensionID` element in their application descriptor
file. If an extension with the specified name is not available, then
`createExtensionContext()` returns `Null`.

To avoid name conflicts, Adobe recommends using reverse DNS for an extension ID.
For example, the ID of the TVControllerChannel extension is
`com.example.TVControllerExtension`. Because all extensions share a single,
global namespace, using reverse DNS for the extension ID avoids name conflicts
between extensions.

## The context type

The method `createExtensionContext()` takes a String parameter that is the
context type for the new extension context. This string specifies more
information about what the new extension context is to do.

For example, suppose the extension com.example.TVControllerExtension can
manipulate both channel and volume settings. Passing `"channel"` or `"volume"`
in `createExtensionContext()` indicates which functionality the new extension
context will be used for. Another ActionScript class in the extension, such as
TVVolumeController, could call `createExtensionContext()` with `"volume"` for
the `contextType` value. The native implementation uses the contextType value in
its context initialization.

Typically, each possible context type value you define corresponds to a
different set of methods in your native implementation. The context type,
therefore, corresponds to what is, in effect, a class in your native
implementation. If you call `createExtensionContext()` multiple times with the
same context type, typically your native implementation creates multiple
instances of a particular native class.

When the context types of multiple calls to `createExtensionContext()` are
different, the native side typically performs different initializations.
Depending on the context type, the native side can create an instance of a
different native class and can provide a different set of native functions.

> Note: A simple extension often has only one context type. That is, it has only
> one set of methods in the native implementation. In this simple case, the
> context type String parameter can be `Null`.
