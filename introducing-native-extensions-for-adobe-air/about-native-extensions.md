# About native extensions

## What is Adobe AIR?

Adobe® AIR® is a cross-operating system runtime that allows content developers
to build rich Internet applications (RIAs). The developers can deploy the RIAs
to the desktop, mobile devices, and digital home devices. AIR applications can
be built using Adobe® Flex® and Adobe® Flash® (SWF-based) and also with HTML,
JavaScript, and Ajax (HTML-based). For more information about the Adobe Flash
Platform tools that you can use to build AIR applications, see
[Adobe Flash Platform tools for AIR development](https://web.archive.org/web/20111212111102/http://help.adobe.com/en_US/air/build/WS2d8d13466044a7337d7adee012406959c52-8000.html)
in
_[Building Adobe AIR Applications](https://web.archive.org/web/20161001085917/http://help.adobe.com/en_US/air/build/index.html)_.

## What is Adobe ActionScript?

SWF-based AIR applications can use Adobe ActionScript® 3.0. ActionScript 3.0 is
an object-oriented language that can add interactivity and data-handling to
RIAs. For more information about the language, see
_[Learning ActionScript 3.0](https://web.archive.org/web/20141012233939/http://help.adobe.com/en_US/as3/learn/index.html)_
and
_[ActionScript 3.0 Developer's Guide](https://web.archive.org/web/20170613023518/http://help.adobe.com/en_US/as3/dev/index.html)_.

ActionScript provides many built-in classes. For example, MovieClip, Array, and
NetConnection are built-in ActionScript classes. Additionally, a content
developer can create application-specific classes. Sometimes an
application-specific class derives from a built-in class.

The runtime executes the code in ActionScript classes. The runtime also executes
JavaScript code that is used in HTML-based applications.

## What is a native extension?

A native extension is a combination of:

- ActionScript classes.

- Native code. Native code is defined here as code that executes outside the
  runtime. For example, code that you write in C is native code. On some
  platforms, Java code is supported in extensions. For the purpose of this
  documentation, this is also considered "native" code.

Reasons to write a native extension include the following:

- A native code implementation provides access to device-specific features.
  These device-specific features are not available in the built-in ActionScript
  classes, and are not possible to implement in application-specific
  ActionScript classes. The native code implementation can provide such
  functionality because it has access to device-specific hardware and software.

- A native code implementation can sometimes be faster than an implementation
  that uses only ActionScript.

- A native code implementation allows you to reuse existing code.

For example, you could create a native extension that allows an application to
do the following:

- make a mobile device vibrate.

- interact with device-specific libraries and features.

When you have finished your ActionScript and native implementations, you package
your extension. Then, an AIR application developer can use the package to call
your extension's ActionScript APIs to execute device-specific functionality. The
extension runs in the same process as the AIR application.

## Native extensions versus the NativeProcess ActionScript class

ActionScript 3.0 provides a NativeProcess class. This class lets an AIR
application execute native processes on the host operating system. This
capability is similar to native extensions, which provide access to
device-specific features and libraries. When deciding on using the NativeProcess
class versus creating a native extension, consider the following:

- Only the `extendedDesktop` AIR profile supports the NativeProcess class.
  Therefore, for applications with the AIR profiles `mobileDevice` and
  `extendedMobileDevice`, native extensions are the only choice.

- Native extension developers often provide native implementations for various
  platforms, but the ActionScript API they provide is typically the same across
  platforms. When using the NativeProcess class, ActionScript code to start the
  native process can vary among the different platforms.

- The NativeProcess class starts a separate process, whereas a native extension
  runs in the same process as the AIR application. Therefore, if you are
  concerned about code crashing, using the NativeProcess class is safer.
  However, the separate process means that you possibly have interprocess
  communication handling to implement.

## Native extensions versus ActionScript class libraries (SWC files)

The most important difference between a native extension and a SWC file is that
the SWC file contains no native code. Therefore, if you determine that you can
accomplish your goal without native code, use a SWC file rather than a native
extension.

## Supported devices

You can create native extensions for the following devices:

- Android devices, starting with AIR 3 and Android 2.2.

- iOS devices, starting with AIR 3 and iOS 4.0

- iOS Simulator, starting with AIR 3.3

- Blackberry PlayBook, starting with AIR 2.7

- Windows desktop devices that support AIR 3.0

- Mac OS X desktop devices that support AIR 3.0

An extension can target multiple platforms. For more information, see
[Targeting multiple platforms](./native-extensions-architecture.md#targeting-multiple-platforms).

## Supported device profiles

The following AIR profiles support native extensions:

- `extendedDesktop`, starting in AIR 3.0

- `mobileDevice`, starting in AIR 3.0

More Help topics

[About SWC files](https://web.archive.org/web/20151111191946/http://help.adobe.com/en_US/flex/using/WS2db454920e96a9e51e63e3d11c0bf69084-7fd3.html)

[AIR profile support](https://web.archive.org/web/20150910215104/http://help.adobe.com/en_US/air/build/WS144092a96ffef7cc16ddeea2126bb46b82f-8000.html)
