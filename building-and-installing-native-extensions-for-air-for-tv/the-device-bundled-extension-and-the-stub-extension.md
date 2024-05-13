# The device-bundled extension and the stub extension

When you write a native extension for an Adobe® AIR® for TV device, you are
required to create two variations of the extension:

- The device-bundled extension, also called the real extension.

- The stub extension.

Furthermore, you can optionally provide a third variation: the simulator
extension.

## The device-bundled extension

The device-bundled extension is the variation that is installed on the device.
The ActionScript side calls functions of the native implementation. You build
this real ActionScript implementation, along with the native implementation,
creating a ZIP file. The device manufacturer unzips this file into a specific
directory on the device.

## The stub extension

A stub native extension has the same ActionScript interfaces as the real
ActionScript implementation, but the ActionScript methods don't do anything. The
stub extension is an ActionScript-only extension; it has no native
implementation. When you build the stub ActionScript implementation, you create
an ANE file.

AIR application developers use this ANE file for three purposes:

- To compile an AIR application that uses the native extension.

- To run the AIR application on a desktop computer, rather than on the target
  device.

- To include in the AIR application package.

## The simulator extension

An optional third variation is a simulator extension. This implementation also
has the same ActionScript interfaces as the real ActionScript implementation.
However, its ActionScript methods simulate the extension's behavior in
ActionScript. Like the stub extension, the simulator extension is an
ActionScript-only extension; it has no native implementation. When you build the
simulator ActionScript implementation, you create an ANE file.

AIR application developers can compile their applications using the simulator
extension ANE file. They can use this ANE file to test the application on a
desktop computer more thoroughly than testing with the stub extension. They can
also include the simulator extension in the AIR application package.

> Note: You can create a simulator extension in place of, or in addition to, the
> stub extension.

## Use of the device-bundled, stub, and simulator extensions

An AIR application developer does the following with the stub and simulator
extensions:

- Uses the stub extension or simulator extension to compile the AIR application.

- Uses the stub extension or simulator extension to test the application on a
  desktop computer.

- Packages the stub extension or simulator extension into their distributable
  AIR application.

  > Note: If you provide both a stub and simulator extension to the AIR
  > application developers, instruct them about which one to package with their
  > distributable application.

When the AIR application runs on the device, AIR for TV does the following:

1.  Looks for the corresponding device-bundled (real) extension on the device.

2.  If it is there, AIR for TV loads it for the AIR application to use.

3.  If it is not there, AIR for TV instead loads the stub or simulator extension
    packaged with the application.
