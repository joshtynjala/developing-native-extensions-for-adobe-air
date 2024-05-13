# Check for native extension support

A best practice is to always define a public interface that provides a handshake
between the native extension and the AIR application. Instruct AIR application
developers using your extension to check this method before calling any other
extension method.

For example, consider an ActionScript extension class public interface called
`isSupported()`. The `isSupported()` method allows an AIR application to make
logic decisions based on whether the device on which the application is running
supports the extension. If `isSupported()` returns `false`, the AIR application
must decide what to do without the extension. For example, the AIR application
can decide to exit.
