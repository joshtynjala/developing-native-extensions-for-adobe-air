# Check for extension support

A best practice is to provide a handshake between the native extension and the
AIR for TV application. The handshake tells the application about the
availability of the extension on the device. This information allows the AIR for
TV application to decide what logic paths to take.

Decide what public interfaces to provide in your ActionScript extension class
for this handshake. Then, instruct AIR for TV application developers on the use
of these interfaces.

For example, consider a native extension that has:

- A stub extension for packaging with the AIR for TV application.

- A simulator extension for testing the application on a desktop computer.

- The device-bundled, real extension for installing on the target device.

In the ActionScript side of each variation, define a method called
`isSupported()` with the following implementations:

- In the real ActionScript implementation that interacts with the native
  implementation, implement the method to return `true`.

  The calling AIR application is running on a device on which the extension is
  device-bundled. Therefore, the application knows it can continue using the
  extension.

- In the stub ActionScript implementation, implement the method to return
  `false`.

  The calling AIR application is running on a device on which the extension is
  not device-bundled. In this situation, AIR for TV uses the stub extension that
  was packaged with the AIR application. The `false` return value informs the
  application not to call any other methods of the extension. The application
  can make the appropriate logic decisions, such as to exit gracefully.

- In a simulator ActionScript implementation, implement the method to return
  `true`.

  The calling AIR application is running on a desktop computer for testing
  purposes. Therefore, the `true` return value informs the application that it
  can continue using the extension.

  However, depending on your extension, you can instruct application developers
  to package their applications with your simulator extension. Then, if the
  application is running on a device that does not have the device-bundled
  extension, the application proceeds with the simulator version of the
  extension.
