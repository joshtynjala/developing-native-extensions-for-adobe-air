# Building an AIR for TV native extension

When you build an AIR for TV native extension, you build two versions of the
extension:

- The device-bundled extension.

- The stub or simulator extension.

The device-bundled extension includes:

- A native implementation, typically written in C or C++.

- The real ActionScript implementation that calls functions of the native
  implementation.

The stub or simulator extension is an ActionScript-only implementation.

For more information on the real, stub, and simulator ActionScript
implementations, see
[The device-bundled extension and the stub extension](./the-device-bundled-extension-and-the-stub-extension.md).

## Creating a signed certificate for the extension

You can choose to digitally sign your native extension. Signing an extension is
optional.

The AIR for TV make utility uses a phony certificate by default. This phony
certificate is useful only for testing. For information about creating a
certificate authority certificate, see
[Creating a signed certificate for a native extension](../packaging-a-native-extension/creating-a-signed-certificate-for-a-native-extension.md).

## Writing the native implementation

For AIR for TV, the native implementation of your extension is an AIR for TV
module. See
_[Optimizing and Integrating Adobe AIR for TV (PDF)](https://web.archive.org/web/20220705165037/http://download.macromedia.com/pub/developer/devices/OptimizingAndIntegratingAdobeAIRForTV.pdf)_
for general information about AIR for TV modules, including details about
building the modules.

The AIR for TV distribution provides an extension development kit (EDK) for
writing and building the native implementation of your extension.

The EDK includes the following:

- The C extension API header file:

      <AIR for TV installation directory>/products/stagecraft/include/ae/edk/FlashRuntimeExtensions.h

  This header file declares the C types and functions that the native
  implementation uses.

- An extension module implementation in the following source file:

      <AIR for TV installation directory>/products/stagecraft/source/ae/edk/ExtensionBridge.cpp

  Do not modify this extension module implementation. When you build your native
  implementation, you must include this source file in your build.

- Makefile support to build your device-bundled extension. For more information,
  see [Creating the .mk file](#creating-the-mk-file) and
  [Running the make utility](#running-the-make-utility).

> **Note:** The AIR for TV EDK requires that the `FREInitializer()` method is
> named `Initializer()` and that the `FREFinalizer()` method is named
> `Finalizer()`. For more information about these methods, see
> [Extension initialization](../coding-the-native-side-with-c/extension-initialization.md)
> and
> [Extension finalization](../coding-the-native-side-with-c/extension-finalization.md).

## Placing ActionScript and native code in the directory structure

Device-bundled extensions are specific to a hardware platform. When you develop
a device-bundled extension, place your files in a subdirectory for your
platform. This subdirectory is in the following directory:

    <AIR for TV installation directory>/products/stagecraft/thirdparty-private/<yourCompany>/stagecraft-platforms/<yourPlatform>/edk

For example, CompanyA uses the following subdirectory for development targeting
their PlatformB:

    <AIR for TV installation directory>/products/stagecraft/thirdparty-private/CompanyA/stagecraft-platforms/PlatformB/edk

Put the header and source files for your C implementation in the
`<yourPlatform>/edk` directory or its subdirectories. For example, put your
extension .cpp and .h files in the following directory:

    <AIR for TV installation directory>/products/stagecraft/thirdparty-private/CompanyA/stagecraft-platforms/PlatformB/edk/myExtension/native

Similarly, put the .as files for your real ActionScript implementation in the
`<yourPlatform>/edk` directory or its subdirectories. For example:

    <AIR for TV installation directory>/products/stagecraft/thirdparty-private/CompanyA/stagecraft-platforms/PlatformB/edk/myExtension/as/real

Also, put the .as files for your stub or simulator ActionScript implementation
in the `<yourPlatform>/edk` directory or its subdirectories. For example:

    <AIR for TV installation directory>/products/stagecraft/thirdparty-private/CompanyA/stagecraft-platforms/PlatformB/edk/myExtension/as/stub
    <AIR for TV installation directory>/products/stagecraft/thirdparty-private/CompanyA/stagecraft-platforms/PlatformB/edk/myExtension/as/simulator

> **Note:** The sample extensions that AIR for TV provides are in the directory
> `<AIR for TV installation directory>/products/stagecraft/source/edk`. Do not
> put your extension files in this directory.

## Creating the .mk file

As with other AIR for TV modules, to build your extensions module, you first
create a .mk file. The primary purpose of the .mk file is to specify the source
files to build.

To create the .mk file:

1.  Copy the PlatformEDKExtension_HelloWorld.mk file or
    PlatformEDKExtension_Process.mk file from:

        <AIR for TV installation directory>/products/stagecraft/source/ae/edk/helloworld/

    or

        <AIR for TV installation directory>/products/stagecraft/source/ae/edk/process/

    Copy it to:

        <AIR for TV installation directory>/products/stagecraft/thirdparty-private/<yourCompany>/stagecraft-platforms/<yourPlatform>

    This directory is the same directory that contains your platform's
    Makefile.config file. See _Creating your platform Makefile.config_ in the
    chapter _Coding, building, and testing_ in
    _[Optimizing and Integrating Adobe AIR for TV (PDF)](https://web.archive.org/web/20220705165037/http://download.macromedia.com/pub/developer/devices/OptimizingAndIntegratingAdobeAIRForTV.pdf)_.

2.  Rename the .mk file to `PlatformEDKExtension_<your extension name>.mk`. The
    AIR for TV make utility automatically discovers .mk files with this naming
    convention.

    Always start the .mk file's name with `PlatformEDKExtension_`.

3.  Edit the sections of the .mk file that are marked "REQUIRED".

Make the following required modifications:

- Set `SC_EDK_EXTENSION_NAME` to the extension name. Set this variable to the
  value of `<your extension name>` in
  `PlatformEDKExtension_<your extension name>.mk`.

- Set `SC_EDK_EXTENSION_PACKAGE` to the extension package name. Set this value
  to the package name you use in the ActionScript side of your extension.

  The make utility uses this value as the value of the `<id>` element in the
  extension's extension descriptor file. It also names the resulting ANE file
  with this value and the .ane filename extension.

  For more information about the extension descriptor file, see
  [Native extension descriptor files](../native-extension-descriptor-files.md).

- Set `SC_EDK_EXTENSION_VERSION` to the version number of the extension.

  The make utility uses this value as the value of the `<versionNumber>` element
  in the extension's extension descriptor file.

- Set `SC_MODULE_SOURCE_DIR`, `SC_MODULE_SOURCE_FILES`, and
  `SC_ADDITIONAL_MODULE_OBJ_SUBDIRS` to specify the native implementation files
  that AIR for TV provides.

  > **Note:** Do not remove ExtensionBridge.cpp from this list. Remove the
  > HelloWorld or Process extension implementation files. Typically, you do not
  > add your extension's source files to this list.

  For example:

      SC_MODULE_SOURCE_DIR := $(SC_SOURCE_DIR_EDK)
      SC_MODULE_SOURCE_FILES := ExtensionBridge.cpp

- Set `SC_PLATFORM_SOURCE_DIR` and `SC_PLATFORM_SOURCE_FILES` to specify the
  native implementation files of your extension. For example:

      SC_PLATFORM_SOURCE_DIR                    := $(SC_PLATFORM_MAKEFILE_DIR)/edk/myExtension/native
      SC_PLATFORM_SOURCE_FILES                     := \
                  MyExtension.cpp \
                  helper\MyHelperClass1.cpp \
                  helper\MyHelperClass2.cpp

- Set `SC_EDK_AS_SOURCE_DIR` to the directory that contains the ActionScript
  files for the real (not the stub) implementation of your extension. For
  example:

      SC_EDK_AS_SOURCE_DIR := $(SC_PLATFORM_MAKEFILE_DIR)/edk/myExtension/as/real

  > **Note:** This directory is the base directory for your ActionScript
  > package. For example, consider an ActionScript package named
  > `tv.adobe.extension.example`. The directories `tv`, `adobe`, `extension`,
  > and `example` are successive subdirectories of `SC_EDK_AS_SOURCE_DIR`.

- Set `SC_EDK_AS_CLASSES` to list every ActionScript class that the real
  ActionScript implementation defines. For example:

      SC_EDK_AS_CLASSES := MyExtension \
                      MyHelperClass1 \
                      MyHelperClass2

- Set `SC_EDK_AS_SOURCE_DIR_AUTHORING` to the directory that contains the
  ActionScript files for the stub or simulator implementation of your extension.
  For example:

      SC_EDK_AS_SOURCE_DIR_AUTHORING := $(SC_PLATFORM_MAKEFILE_DIR)/edk/myExtension/as/stub

  > **Note:** This directory is the base directory for your ActionScript
  > package. For example, consider an ActionScript package named
  > `tv.adobe.extension.example`. The directories `tv`, `adobe`, `extension`,
  > and `example` are successive subdirectories of
  > `SC_EDK_AS_SOURCE_DIR_AUTHORING`.

- Set `SC_EDK_AS_CLASSES_AUTHORING` to list every ActionScript class that the
  stub or simulator ActionScript implementation defines. For example:

      SC_EDK_AS_CLASSES_AUTHORING := MyExtension \
                      MyHelperClass1 \
                      MyHelperClass2

## Install third-party libraries

Building AIR for TV requires some third-party libraries. Details on these
libraries are in _Install third-party software_ in
_[Getting Started with Adobe AIR for TV (PDF)](https://web.archive.org/web/20220705161131/http://download.macromedia.com/pub/developer/devices/GettingStartedWithAdobeAIRForTV.pdf)_.

If you are building only your extension module, and not building all of AIR for
TV, the necessary libraries are:

- The AIR SDK

  Select the Mac OS X download from <https://airsdk.harman.com/>.

  Create a directory to contain the .tbz2 file's contents. For example:

      /usr/AIRSDK

  Extract the .tbz2 file's contents into the directory.

      tar jxf AdobeAIRSDK.tbz2

  Set the `PATH` environment variable to include the AIR SDK bin directory. In
  this example, the bin directory is /usr/AIRSDK/bin.

- The Open Source Flex® SDK.

  Download the ZIP file of the latest release build of the Open Source Flex SDK
  from <http://opensource.adobe.com/wiki/display/flexsdk/Downloads>.

  Create a directory to contain the ZIP file's contents. For example:

      /usr/flexSDK

  Extract the ZIP file's contents into the directory.

      unzip flex_sdk_4.5.1.21328_mpl.zip

  Set the `PATH` environment variable to include the Flex SDK bin directory. In
  this example, the bin directory is /usr/flexSDK/bin.

- The Java™ runtime. The Flex SDK requires a recent Java runtime. If your
  development system does not yet have a Java runtime, downloads and
  installation instructions are at [https://openjdk.org/](https://openjdk.org/).

  Set the `PATH` environment variable to include the Java bin directory.

## Running the make utility

Details on using the AIR for TV make utility are in:

- _[Getting Started with Adobe AIR for TV (PDF)](https://web.archive.org/web/20220705161131/http://download.macromedia.com/pub/developer/devices/GettingStartedWithAdobeAIRForTV.pdf)_
  in the chapter _Installing and building the source distribution_.

- _[Optimizing and Integrating Adobe AIR for TV (PDF)](https://web.archive.org/web/20220705165037/http://download.macromedia.com/pub/developer/devices/OptimizingAndIntegratingAdobeAIRForTV.pdf)_
  in the chapter _Coding, building, and testing._ Follow the instructions in the
  section called _Creating your platform Makefile.config_ to set the various
  build variables.

In particular, the make utility uses the following build variables in
Makefile.config when building extensions:

- `SC_ZIP`

- `SC_UNZIP`

- `SC_PLATFORM_NAME`

- `SC_PLATFORM_ARCH`

After you have created your platform's Makefile.config file and your extension's
.mk file, you can use the make utility to do the following:

- Build all of AIR for TV.

- Build only your extension module.

To build all of AIR for TV, do the following:

1.  Make sure the environment variables `SC_BUILD_MODE` and `SC_PLATFORM` are
    set.

2.  If you are using a certificate that you created to sign your extension, set
    the environment variables `SC_EDK_ANE_CERT_FILE` and
    `SC_EDK_ANE_CERT_PASSWD`.

    Set `SC_EDK_ANE_CERT_FILE` to the relative or absolute path to your
    certificate. The relative path is relative to the build directory \< _AIR
    for TV installation directory_ \>/stagecraft/build/linux.

    Set `SC_EDK_ANE_CERT_PASSWD` to the password of the certificate.

    If you do not set these environment variables, the make utility uses a
    default phony certificate, and displays a warning message. This phony
    certificate is appropriate only for your testing.

3.  Change to the directory:

        <AIR for TV installation directory>/products/stagecraft/build/linux

4.  Enter the following command:

        make

To build only your extension module, do the following:

1.  Make sure the environment variables `SC_BUILD_MODE` and `SC_PLATFORM` are
    set.

2.  If you are using a certificate that you created to sign your extension, set
    the environment variables `SC_EDK_ANE_CERT_FILE` and
    `SC_EDK_ANE_CERT_PASSWD` as described in the previous steps.

3.  Change to the directory stagecraft/build/linux.

4.  Enter the following command:

        make PlatformEDKExtension_<your extension name>

You can remove all objects previously built for your extension with the
following command:

    make clean-PlatformEDKExtension_<your extension name>

You can remove all objects previously built for your extension and then rebuild
them with the following command:

    make rebuild-PlatformEDKExtension_<your extension name>

Important: The make utility sometimes fails if your build machine is behind a
firewall. A firewall can prohibit access to the time-stamp server that ADT uses
when it packages the native extension into an ANE file. This failure results in
the following error output:

    Could not generate timestamp: Connection timed out

To work around this failure, modify the ADT command that the make utility uses.
Edit the file extension.mk in the following directory:

    <AIR for TV installation directory>/stagecraft/source/ae/edk/

Find the following line:

    $(SC_EXEC_CMD) $(SC_ADT) -package \

Add the parameter `-tsa none` to the command as follows:

    $(SC_EXEC_CMD) $(SC_ADT) -package -tsa none\

## Make utility extension output

The make utility creates two files for your extension. It puts the files in one
of the following directories depending on whether you specified debug or release
for `SC_BUILD_MODE`:

    <AIR for TV installation directory>/build/stagecraft/linux/<yourPlatform>/debug/bin
    <AIR for TV installation directory>/build/stagecraft/linux/<yourPlatform>/release/bin

The files that the make utility creates for your extension are:

- A ZIP file that contains the device-bundled extension to deploy on the device.

- An ANE file that contains the stub or simulator extension. AIR application
  developers use this ANE file to build their applications. They also use it to
  test their applications on a desktop computer using ADL. They also package
  this ANE file with their application into an AIRN package.

## Building both a stub and simulator extension

Sometimes you want to build both a stub and a simulator extension, in addition
to the real extension. Typically, you instruct the AIR application developers to
do the following:

- Test on the desktop using the simulator extension.

- Package the stub extension with their application into an AIRN package.

To build both a stub and simulator extension, do the following:

1.  Create the stub extension and its .mk file. Make sure you can build the stub
    extension and the real extension.

2.  Create a directory for your simulator implementation that is a sibling of
    your stub implementation directory. For example:

        <AIR for TV installation directory>/products/stagecraft/thirdparty-private/CompanyA/stagecraft-platforms/PlatformB/edk/myExtension/as/stub
        <AIR for TV installation directory>/products/stagecraft/thirdparty-private/CompanyA/stagecraft-platforms/PlatformB/edk/myExtension/as/simulator

3.  Make a copy of the .mk file for your extension.

4.  In the copy, edit the values of `SC_EDK_AS_SOURCE_DIR_AUTHORING` and
    `SC_EDK_AS_CLASSES_AUTHORING`. Set the values to reflect your simulator
    implementation directory and classes.

5.  Rename the original .mk file for your extension to keep it safe. Then,
    rename the copy to the .mk filename for your extension:
    `PlatformEDKExtension_<your extension name>.mk`.

6.  Move the stub ANE file in your platform's bin directory to a safe place.
    Otherwise, the next step overwrites it.

7.  Run the make utility to build the real extension and your simulator
    extension.
