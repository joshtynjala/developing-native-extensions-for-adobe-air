# Dispatching asynchronous events

The native C code can dispatch asynchronous events back to the ActionScript side
of your extension. For example, an extension method can start another thread to
perform some task. When the task in the other thread completes, that thread
calls `FREDispatchStatusEventAsync()` to inform the ActionScript side of the
extension. The target of the event is an ActionScript ExtensionContext instance.

The sequence diagram in [Extension functions](./extension-functions.md) shows a
native C function starting an asynchronous thread, which later dispatches an
event.

More Help topics

[FREDispatchStatusEventAsync()](../native-c-api-reference/functions-you-use/fredispatchstatuseventasync.md)
