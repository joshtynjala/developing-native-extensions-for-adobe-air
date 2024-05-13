# AIR for TV extension examples

Adobe® AIR® for TV provides several examples of native extensions. The native
implementation is written in C++ and uses the AIR for TV extensions development
kit (EDK). The EDK is distributed to device manufacturers and system-on-a-chip
manufacturers who include AIR for TV with their product. More information about
the AIR for TV EDK and creating AIR for TV extensions is in
[Building an AIR for TV native extension](./building-an-air-for-tv-native-extension.md).

As an AIR for TV extension developer, you can:

- Copy these examples as starting point for your extension.

- See these examples for code samples that show how to use various C API
  extension functions as well as the ActionScript ExtensionContext class.

- Copy the makefile of one of these examples as a starting point for creating
  the makefile for your extension.

<!-- -->

## HelloWorld example

The HelloWorld example is in the following directory of the AIR for TV
distribution:

    <AIR for TV installation directory>/products/stagecraft/source/ae/edk/helloworld

The HelloWorld example is a simple extension to illustrate basic extension
behavior. It does the following:

- Uses the `ExtensionContext.call()` method to pass a string from the
  ActionScript side to the native implementation.

- Returns a string from the native implementation to the ActionScript side.

- Starts a thread in the native implementation that sends asynchronous events to
  the ActionScript side.

The following table describes each file and its location relative to the
`helloworld/` directory:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>File</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HelloWorld.as</p>
<p>in directory</p>
<p>as/device/src/tv/adobe/extension/example/</p></td>
<td><p>ActionScript side of the real (not the stub) extension that
defines the HelloWorld class. It does the following:</p>
<div>
<ul class="incremental">
<li><p>Creates an ExtensionContext instance.</p></li>
<li><p>Defines the extension's ActionScript APIs: <samp>Hello()</samp>
and <samp>StartCount()</samp>.</p></li>
<li><p>Listens for events on the ExtensionContext instance, and
redispatches the events to the HelloWorld instance's listeners.</p></li>
</ul>
</div></td>
</tr>
<tr class="even">
<td><p>HelloWorld.as</p>
<p>in directory</p>
<p>as/distributable/src/tv/adobe/extension/example/</p></td>
<td><p>ActionScript of the stub extension that defines the HelloWorld
class. This ActionScript-only stub defines the extension's ActionScript
APIs: <samp>Hello()</samp> and <samp>StartCount()</samp>. However, the
stub implementations do not call native functions.</p></td>
</tr>
<tr class="odd">
<td><p>HelloWorldExtensionClient.as</p>
<p>in directory</p>
<p>client/src</p></td>
<td><p>AIR application that uses the extension. The AIR application is
the client of the extension. It does the following:</p>
<div>
<ul class="incremental">
<li><p>Creates an instance of the HelloWorld class.</p></li>
<li><p>Listens for events on the HelloWorld instance.</p></li>
<li><p>Calls the HelloWorld instance's <samp>Hello()</samp> and
<samp>StartCount()</samp> APIs.</p></li>
</ul>
</div></td>
</tr>
<tr class="even">
<td><p>HelloWorldExtensionClient-app.xml</p>
<p>in directory</p>
<p>client/src</p></td>
<td><p>AIR application descriptor file. Includes the
<samp>&lt;extensions&gt;</samp> element with the
<samp>extensionID</samp> value
<samp>tv.adobe.extension.example.HelloWorld</samp>.</p></td>
</tr>
<tr class="odd">
<td><p>HelloWorld.h</p>
<p>in directory</p>
<p>native/</p></td>
<td><p>The C++ header file of the HelloWorld class.</p></td>
</tr>
<tr class="even">
<td><p>HelloWorld.cpp</p>
<p>in directory</p>
<p>native/</p></td>
<td><p>The C++ implementation file of the HelloWorld class. The
implementation does the following:</p>
<div>
<ul class="incremental">
<li><p>Defines the FREFunction <samp>Hello()</samp> which writes its
string parameter to the console. It also returns the string "Hello from
extensionland".</p></li>
<li><p>Defines the FREFunction <samp>StartCount()</samp> which starts an
asynchronous thread to send one event every 500 milliseconds to the
ExtensionContext instance.</p></li>
</ul>
</div></td>
</tr>
<tr class="odd">
<td><p>HelloWorldExtension.cpp</p>
<p>in directory</p>
<p>native/</p></td>
<td><p>Contains implementations of the following C API extension
functions:</p>
<div>
<ul class="incremental">
<li><p><samp>FREInitializer()</samp></p></li>
<li><p><samp>FREContextInitializer()</samp></p></li>
<li><p><samp>FREContextFinalizer()</samp></p></li>
<li><p><samp>FREFinalizer()</samp></p></li>
</ul>
</div></td>
</tr>
<tr class="even">
<td><p>PlatformEDKExtension_HelloWorld.mk</p></td>
<td><p>The makefile for the HelloWorld extension.</p></td>
</tr>
<tr class="odd">
<td><p>ExtensionUtil.h</p>
<p>in directory</p>
<p><em>&lt;AIR for TV installation directory&gt;</em>
/products/stagecraft/source/ae/edk</p></td>
<td><p>Contains macros convenient to coding your C or C++
implementation.</p></td>
</tr>
<tr class="even">
<td><p>ExtensionBridge.cpp</p>
<p>in directory</p>
<p><em>&lt;AIR for TV installation directory&gt;</em>
/products/stagecraft/source/ae/edk</p></td>
<td><p>The AIR for TV extension module implementation. When you build
your native implementation, include this source file in your
build.</p></td>
</tr>
<tr class="odd">
<td><p>phonyEdkAneCert.p12</p>
<p>in directory</p>
<p><em>&lt;AIR for TV installation directory&gt;</em>
/products/stagecraft/source/ae/edk</p></td>
<td><p>A phony certificate that the make utility uses for packaging the
HelloWorld extension into an ANE file.</p></td>
</tr>
<tr class="even">
<td><p>extension.mk</p>
<p>in directory</p>
<p><em>&lt;AIR for TV installation directory&gt;</em>
/products/stagecraft/source/ae/edk</p></td>
<td><p>The makefile for the extension module. Do not modify this
file.</p></td>
</tr>
</tbody>
</table>

## Process example

The Process example is in the following directory of the AIR for TV
distribution:

    <AIR for TV installation directory>/products/stagecraft/source/ae/edk/process

The Process extension allows an AIR application to manipulate Linux processes,
including the following functionality:

- Spawning a Linux process. The process executes a Linux command that the AIR
  application specifies.

- Getting the process identifier of the process.

- Checking whether the process has completed.

- Receiving an event that the process has completed.

- Getting the return code from the completed process.

- Receiving events indicating that the process has written to `stdout` or
  `stderr`.

- Retrieving the output strings from `stdout` and `stderr`.

- Writing strings to `stdin`.

- Sending an interrupt signal to the process.

- Killing the process.

The following table describes each file and its location relative to the
`process/` directory:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>File</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Process.as</p>
<p>in directory</p>
<p>as/device/src/tv/adobe/extension/process/example/</p></td>
<td><p>ActionScript side of the real (not the stub) extension that
defines the Process class. It does the following:</p>
<div>
<ul class="incremental">
<li><p>Creates an ExtensionContext instance.</p></li>
<li><p>Defines the extension's ActionScript APIs.</p></li>
<li><p>Listens for events on the ExtensionContext instance, and
redispatches the events to the Process instance's listeners.</p></li>
</ul>
</div></td>
</tr>
<tr class="even">
<td><p>ProcessEvent.as</p>
<p>in directory</p>
<p>as/device/src/tv/adobe/extension/process/example/</p></td>
<td><p>Defines the ProcessEvent class, which derives from the Event
class.</p>
<p>The AIR application ActionScript listens for these ProcessEvent
notifications.</p></td>
</tr>
<tr class="odd">
<td><p>Process.as</p>
<p>in directory</p>
<p>as/distributable/src/tv/adobe/extension/process/example/</p></td>
<td><p>ActionScript of the stub extension that defines the Process
class. This ActionScript-only stub defines the extension's ActionScript
APIs. However, the stub implementations do not call native
functions.</p></td>
</tr>
<tr class="even">
<td><p>ProcessExtensionClient.as</p>
<p>in directory</p>
<p>client/simple/src</p></td>
<td><p>AIR application that uses the extension. The AIR application is
the client of the extension. It provides an example of how an AIR
application uses the Process extension APIs.</p></td>
</tr>
<tr class="odd">
<td><p>ProcessExtensionClient-app.xml</p>
<p>in directory</p>
<p>client/simple/src</p></td>
<td><p>AIR application descriptor file. Includes the
<samp>&lt;extensions&gt;</samp> element with the
<samp>extensionID</samp> value
<samp>tv.adobe.extension.process.Process</samp>.</p></td>
</tr>
<tr class="even">
<td><p>Process.h</p>
<p>in directory</p>
<p>native/</p></td>
<td><p>The C++ header file of the abstract Process class.</p></td>
</tr>
<tr class="odd">
<td><p>ProcessLinux.h</p>
<p>in directory</p>
<p>native/</p></td>
<td><p>The C++ header file of the concrete ProcessLinux class.</p>
<p>The ProcessLinux class derives from the Process class. It declares
private methods and data for a Linux implementation of the Process
class.</p></td>
</tr>
<tr class="even">
<td><p>ProcessLinux.cpp</p>
<p>in directory</p>
<p>native/</p></td>
<td><p>The C++ implementation file of the ProcessLinux class. The
implementation includes the following functionality:</p>
<div>
<ul class="incremental">
<li><p>Defines the FREFunction functions. These functions use Linux
system calls to, for example, fork and exec a Linux process and to
interact with <samp>stdin</samp>, <samp>stdout</samp>, and
<samp>stderr</samp></p></li>
<li><p>Monitors the status of the spawned process. The implementation
creates a thread for this purpose. The thread uses the C extension API
<samp>FREDispatchStatusEventAsync()</samp> to report events.</p></li>
<li><p>Defines helper functions for creating FREObject variables for
returning information from the FREFunction functions to the ActionScript
side. These helper functions use C API extension functions such as
<samp>FRENewObjectFromBool()</samp>,
<samp>FRENewObjectFromUTF8()</samp>, and
<samp>FRENewObjectFromUint32()</samp>.</p></li>
</ul>
</div></td>
</tr>
<tr class="odd">
<td><p>ProcessExtension.cpp</p>
<p>in directory</p>
<p>native/</p></td>
<td><p>Contains implementations of the following C API extension
functions:</p>
<div>
<ul class="incremental">
<li><p><samp>FREInitializer()</samp></p></li>
<li><p><samp>FREContextInitializer()</samp></p></li>
<li><p><samp>FREContextFinalizer()</samp></p></li>
<li><p><samp>FREFinalizer()</samp></p></li>
</ul>
</div></td>
</tr>
<tr class="even">
<td><p>PlatformEDKExtension_Process.mk</p></td>
<td><p>The makefile for the Process extension.</p></td>
</tr>
<tr class="odd">
<td><p>ExtensionUtil.h</p>
<p>in directory</p>
<p><em>&lt;AIR for TV installation directory&gt;</em>
/products/stagecraft/source/ae/edk</p></td>
<td><p>Contains macros convenient to coding your C or C++
implementation.</p></td>
</tr>
<tr class="even">
<td><p>ExtensionBridge.cpp</p>
<p>in directory</p>
<p><em>&lt;AIR for TV installation directory&gt;</em>
/products/stagecraft/source/ae/edk</p></td>
<td><p>The AIR for TV extension module implementation. When you build
your native implementation, include this source file in your
build.</p></td>
</tr>
<tr class="odd">
<td><p>phonyEdkAneCert</p>
<p>in directory</p>
<p><em>&lt;AIR for TV installation directory&gt;</em>
/products/stagecraft/source/ae/edk</p></td>
<td><p>A phony certificate that the make utility uses for packaging the
Process extension into an ANE file.</p></td>
</tr>
<tr class="even">
<td><p>extension.mk</p>
<p>in directory</p>
<p><em>&lt;AIR for TV installation directory&gt;</em>
/products/stagecraft/source/ae/edk</p></td>
<td><p>The makefile for the extension module. Do not modify this
file.</p></td>
</tr>
</tbody>
</table>

## Build the extension examples on the x86Desktop platform

To build the Hello World or Process extension example on the x86Desktop
platform, first build your AIR for TV distribution for the x86Desktop platform.
Instructions are in
_[Getting Started with Adobe AIR for TV (PDF)](https://web.archive.org/web/20220705161131/http://download.macromedia.com/pub/developer/devices/GettingStartedWithAdobeAIRForTV.pdf)_
in _Quick Start on Linux_.

> Note: Make sure that you installed the AIR 3 SDK, the The Open Source Flex®
> SDK, and the Java™ runtime, and included the bin directories in your PATH
> environment variable. Building native extensions for AIR for TV depends on
> these libraries.

Next, add building the Hello World or Process extension example to your
x86Desktop build. Do the following:

1.  Change to the directory:

        <AIR for TV installation directory>/products/stagecraft/build/linux/platforms/x86Desktop

2.  Link to the .mk file of the extension you want to build. For example:

        ln -s <AIR for TV installation directory>/products/stagecraft/source/ae/edk/helloworld/PlatformEDKExtension_HelloWorld.mk

3.  Change to the directory:

         <AIR for TV installation directory>/products/stagecraft/build/linux

4.  Build the distribution, including the extension example:

        make

    Alternatively, build only the extension example. For example:

        make PlatformEDKExtension_HelloWorld.mk

The make utility creates two files for each extension example. It puts the files
in one of the following directories depending on whether you specified debug or
release for `SC_BUILD_MODE`:

    <AIR for TV installation directory>/build/stagecraft/linux/x86Desktop/debug/bin
    <AIR for TV installation directory>/build/stagecraft/linux/x86Desktop/release/bin

The files that the make utility creates for the example extension are:

- A ZIP file that contains the device-bundled extension.

- An ANE file that contains the stub or simulator extension.
