# Creating the native extension package

To provide your native extension to application developers, you package all the
related files into an ANE file. The ANE file is an archive file that contains:

- The extension's ActionScript library

- The extension's native code library

- The extension descriptor file

- The extension's certificate

- The extension's resources, such as images.

Use the AIR Developer Tool (ADT) to create the ANE file. Complete documentation
for ADT is at
[AIR Developer Tool](https://web.archive.org/web/20160326215330/http://help.adobe.com/en_US/air/build/WS5b3ccc516d4fbf351e63e3d118666ade46-7fd9.html).

## ADT example for packaging an extension

The following example illustrates how to package an ANE file with ADT. The
example packages the ANE file to use with applications that:

- Run on Android devices.

- Run on Android x86 devices.

- Run on iOS devices.

- Run on the iOS Simulator.

- Run on tvOS devices.

- Run on the tvOS Simulator.

- Run on other devices using the default ActionScript-only implementation.

<!-- -->

    adt -package <signing options> -target ane MyExtension.ane MyExt.xml -swc MyExtension.swc     -platform Android-ARM -C platform/Android .
                        -platform Android-x86 -C platform/Android-x86 .
                        -platform iPhone-ARM -platformoptions platform.xml
                        abc/x.framework lib.o -C platform/ios .
                        -platform iPhone-x86 -C platform/iosSimulator .
                        -platform appleTV-ARM -platformoptions platformtv.xml
                        abc/x.framework lib.o -C platform/tvos .
                        -platform appleTV-x86 -C platform/tvosSimulator .
                        -platform default -C platform/default library.swf

In this example, the following command-line options are used to create the ANE
package:

- _\<signing options\>_

  You can optionally sign the ANE file. For more information, see
  [Creating a signed certificate for a native extension](./creating-a-signed-certificate-for-a-native-extension.md).

- `-target ane`

  The `-target` flag specifies which type of package to create. Use the `ane`
  target to package a native extension.

- `MyExtension.ane`

  Specify the name of the package file to create. Use the .ane filename
  extension.

- `MyExt.xml`

  Specify the extension descriptor file. The file specifies the extension ID and
  supported platforms. AIR uses this information to locate and load an extension
  for an application. In this example, the extension descriptor is:

      <extension xmlns="http://ns.adobe.com/air/extension/3.1">
          <id>com.sample.ext.MyExtension</id>
          <versionNumber>0.0.1</versionNumber>
          <platforms>
              <platform name="Android-ARM">
                  <applicationDeployment>
                      <nativeLibrary>MyExtension.jar</nativeLibrary>
                      <initializer>com.sample.ext.MyExtension</initializer>
                  </applicationDeployment>
              </platform>
              <platform name="Android-x86">
                  <applicationDeployment>
                      <nativeLibrary>MyExtension.jar</nativeLibrary>
                      <initializer>com.sample.ext.MyExtension</initializer>
                  </applicationDeployment>
              </platform>
              <platform name="iPhone-ARM">
                  <applicationDeployment>
                      <nativeLibrary>MyExtension.a</nativeLibrary>
                      <initializer>InitMyExtension></initializer>
                  </applicationDeployment>
              </platform>
              <platform name="iPhone-x86">
                  <applicationDeployment>
                      <nativeLibrary>MyExtension.a</nativeLibrary>
                      <initializer>InitMyExtension></initializer>
                  </applicationDeployment>
              </platform>
              <platform name="appleTV-ARM">
                  <applicationDeployment>
                      <nativeLibrary>MyExtension.a</nativeLibrary>
                      <initializer>InitMyExtension></initializer>
                  </applicationDeployment>
              </platform>
              <platform name="appleTV-x86">
                  <applicationDeployment>
                      <nativeLibrary>MyExtension.a</nativeLibrary>
                      <initializer>InitMyExtension></initializer>
                  </applicationDeployment>
              </platform>
              <platform name="default">
                  <applicationDeployment/>
              </platform>
          </platforms>
      </extension>

  See
  [Native extension descriptor files](../native-extension-descriptor-files.md)
  for more information.

- `MyExtension.swc`

  Specify the SWC file that contains the ActionScript side of the extension.

- `platform Android-ARM -C platform/Android . -platform Android-x86 -C platform/Android-x86 . -platform iPhone-ARM -platformoptions platform.xml -C platform/iOS . -platform appleTV-ARM -platformoptions platformtv.xml -C platform/tvos .`

  The `-platform` flag names a platform that this ANE file supports. The options
  that follow the name specify where to find the platform-specific libraries and
  resources. In this case, the `-C` option for the `Android-ARM` platform
  indicates to make the relative directory `platform/Android` the working
  directory. The directories and files that follow are relative to the new
  working directory.

  Therefore, in this example, the relative directory `platform/Android` contains
  all the Android native code library and resources. It also contains the
  Android platform-specific library.swf file and any other Android
  platform-specific SWF files.

  The `-platformoptions` flag for the iPhone-ARM/appleTV-ARM platform is an
  optional entry that lets you specify platform-specific options. These options
  include options for linking to iOS/tvOS frameworks (other than the default
  ones) as well as bundling third-party static libraries with your native
  extension. See
  [iOS native libraries](./building-the-native-library.md#ios-native-libraries).

- `-platform default -C platform/default library.swf`

  When the `-platform` option names the `default` platform, do not specify any
  native code files. Specify only a library.swf file, as well as other SWF
  files, if any.

## The SWC file and SWF files in the ANE package

You specify a SWC file in the `-swc` option of the ADT packaging command. This
SWC file is your ActionScript library. It contains a file called library.swf.
ADT puts the library.swf from the SWC file into the ANE file. When an AIR
application uses a native extension, it includes the extension's ANE file in its
library path so that the application can compile. In fact, the application
compiles against the public interfaces in library.swf.

Sometimes you create a different ActionScript implementation for each target
platform. In this case, compile a SWC file for each platform and put the
library.swf file from each SWC file in the appropriate platform directory before
using the ADT packaging command. You can extract library.swf from a SWC file
with extraction tools such as WinZip.

Consider the case when your extension's public interfaces are the same across
all platforms. In this case, it doesn't matter which of the platform-specific
SWC files you use in the `-swc` option of the ADT command. It doesn't matter
because the SWF file in the SWC file is used only for application compilation.
The SWF file that you put in the platform directory is the file that the native
extension uses when it runs.

Note the following about the library.swf file:

- ADT requires that you provide a main SWF file named library.swf for each
  platform. When you create a SWC file, library.swf is the name of the SWF file.

- The library.swf file for each platform can be different.

- The library.swf file for each platform can be the same if the ActionScript
  side has no platform dependencies.

- The library.swf for each platform can load other SWF files that you include in
  the platform-specific directory. These other SWF files can have any name.

## ANE file rules for application packaging

Use ADT to package applications that use native extensions. When you package an
application that uses an extension, ADT verifies that there is a platform
specified in the ANE file that matches the application packaging target . For
example, the platform `Android-ARM` matches an Android apk package.

Furthermore, ADT matches the `default` platform with _any_ target package. The
`default` platform specifies an ActionScript-only version of the extension.
Consider an AIR application that uses an application-bundled extension. AIR
loads the ActionScript library of the `default` platform extension only if none
of the extension's specified platforms correspond to the device.

For example, consider an application-bundled extension that specifies the
platforms `iPhone-ARM`, `Android-ARM`, and `default`. When the application using
the extension runs on a Windows platform, it uses the extension's `default`
platform library.

Therefore, when you create an ANE file for application-bundling, consider the
following rules that ADT uses when packaging an application that uses the ANE
file:

- To create an Android application package, the ANE file must include the
  `Android-ARM` platform. Alternatively, the ANE file must include the default
  platform and at least one other platform.

- To create an iOS application package, the ANE file must include the
  `iPhone-ARM` platform. Alternatively, the ANE file must include the default
  platform and at least one other platform.

- To create an iOS Simulator application package, the ANE file must include the
  `iPhone-x86` platform. Alternatively, the ANE file must include the default
  platform and at least one other platform.

- To create a tvOS application package, the ANE file must include the
  `appleTV-ARM` platform. Alternatively, the ANE file must include the default
  platform and at least one other platform.

- To create a tvOS Simulator application package, the ANE file must include the
  `appleTV-x86` platform. Alternatively, the ANE file must include the default
  platform and at least one other platform.

- To create a Mac OS X application package, the ANE file must include the
  `MacOS-x86-64` platform. Alternatively, the ANE file must include the default
  platform and at least one other platform.

- To create a Windows application package, the ANE file must include the
  `Windows-x86` platform. Alternatively, the ANE file must include the default
  platform and at least one other platform.

Only one platform implementation is ever bundled with an application. However,
when you test an application containing an extension using the ADL utility, then
the implementation is chosen at run time. This run-time selection can lead to
differences in behavior depending on the test platform and the ANE package. For
example, if the ANE includes implementations for the `Android-ARM`,
`Windows-x86`, and `default` platforms, the implementation used when testing is
different depending on whether the test computer is running Windows or OS X. On
Windows, the `Windows-x86` platform implementation is used (even when testing
under the mobile profile); on OS X, the `default` implementation is used.

## Including additional Android shared .so libraries in the ANE package

Consider a native extension that targets the platform `Android-ARM`. The primary
library of the native side of the extension is either:

- a .so library if you use the Android NDK

- a JAR file if you use the Android SDK

Sometimes, however, the native side requires more native libraries (.so
libraries) than the primary .so library or JAR file for the extension.

For example:

- You are using the Java API to develop your native extension. However, you want
  to use the JNI (Java Native Interface) to access native .so libraries from
  your Java code.

- You are using the C API to develop your native extension. However, you want to
  partition your code into multiple shared libraries. Based on your extension's
  logic, you want to load the appropriate shared .so library at runtime.

When you create the ANE package, use the following directory structure:

    <Android platform directory>/
            libs/
            armeabi/
            <Android emulator native libraries>
            armeabi-v7a/
            <Android device native libraries>

When you use ADT to create the ANE package, set the `-platform` option to
specify the Android platform directory contents:

    -platform Android-ARM -C <Android platform directory>.

When an application developer uses ADT to include the ANE package in an APK
package, the APK package includes the following libraries:

- The libraries in `libs/armeabi-v7a` if the ADT target is `apk` or
  `apk-captive-runtime`.

- The libraries in `libs/armeabi` if the ADT target is `apk-emulator`,
  `apk-debug`, or `apk-profile`.

> Note: For the iPhone-ARM platform, you cannot include shared libraries in your
> ANE file. For more information, see
> [Building the native library](./building-the-native-library.md).
