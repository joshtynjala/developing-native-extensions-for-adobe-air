# Dispatching asynchronous events

The Java code can dispatch asynchronous events back to the ActionScript code of
your extension. For example, an extension method can start another thread to
perform some task. When the task in the other thread completes, that thread
calls the `dispatchStatusEventAsync()` method of the appropriate
[FREContext](../android-java-api-reference/classes/frecontext.md). On the
ActionScript side, the ActionScript ExtensionContext instance associated with
that Java FREContext dispatches a Status event.
