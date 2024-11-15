# Creating the extension descriptor file

Each native extension contains an extension descriptor file. This XML file
specifies information about the extension, such as the extension identifier,
name, version number, and the platforms that it can run on.

When creating extensions, write the extension descriptor file according to the
detailed schema
[Native extension descriptor files](../native-extension-descriptor-files.md).

For example:

    <extension xmlns="http://ns.adobe.com/air/extension/3.5">
        <id>com.example.MyExtension</id>
        <versionNumber>0.0.1</versionNumber>
        <platforms>
            <platform name="Android-ARM">
                <applicationDeployment>
                    <nativeLibrary>MyExtension.jar</nativeLibrary>
                    <initializer>com.sample.ext.MyExtension</initializer>
                </applicationDeployment>
            </platform>
            <platform name="iPhone-ARM">
                <applicationDeployment>
                    <nativeLibrary>MyExtension.a</nativeLibrary>
                    <initializer>MyExtensionIntializer</initializer>
                </applicationDeployment>
            </platform>
            <platform name="default">
                <applicationDeployment/>
            </platform>
        </platforms>
    </extension>

Consider the following information when creating your extension descriptor file.

#### The extension ID

The value of the `<id>` element is the same value used in:

- the ActionScript call to `CreateExtensionContext()`.

- the `extensionID` element in the application descriptor file of an application
  that uses the extension.

For best practices for naming the extension ID, see
[The extension ID](../coding-the-actionscript-side/create-an-extensioncontext-instance.md#the-extension-id).

#### The version number

The value of the `<versionNumber>` element is for specifying the version of the
extension. One important use of the version number is for maintaining backward
compatibility on device-bundled extensions. See
[Native extension backward compatibility](../coding-the-actionscript-side/native-extension-backward-compatibility.md).

#### Platforms

You can write a native extension that targets multiple platforms as discussed in
[Targeting multiple platforms](../introducing-native-extensions-for-adobe-air/native-extensions-architecture.md#targeting-multiple-platforms).

Depending on the platform, the extension is either application-bundled or
device-bundled, as discussed in
[Extension availability at runtime](../introducing-native-extensions-for-adobe-air/native-extensions-architecture.md#extension-availability-at-runtime).

For each targeted platform, provide a
[`<platform>`](../native-extension-descriptor-files.md#platform) element in the
extension descriptor file. The `<platform>` element's `name` attribute specifies
the target platform, such as `iPhone-ARM` or `Windows-x86`. Application-bundled
extensions can also specify `default` for the `name` attribute value. This value
indicates that the extension is an ActionScript-only extension; the extension
has no native code libraries.

When an AIR application that uses an application-bundled extension runs, AIR
does the following:

- AIR loads the extension libraries that the extension descriptor file
  associates with the platform name that corresponds to the device's platform.

- If no platform name corresponds to the device, AIR loads the extension
  libraries that the extension descriptor file associates with the default
  platform.

#### Descriptor namespace

The namespace specified in the root `<extension>` element of the descriptor file
determines the version of the AIR SDK required by the extension. The namespace
is one of the factors, along with SWF version, that determine whether an
extension can be used in an AIR application. The AIR application descriptor
namespace must be greater than or equal to the extension descriptor namespace.

| Extension namespace value      | Compatible AIR version | ANE SWF version |
| ------------------------------ | ---------------------- | --------------- |
| ns.adobe.com/air/extension/2.5 | AIR 3+                 | 13              |
| ns.adobe.com/air/extension/3.1 | AIR 3.1+               | 14              |
| ns.adobe.com/air/extension/3.2 | AIR 3.2+               | 15              |
| ns.adobe.com/air/extension/3.3 | AIR 3.3+               | 16              |
| ns.adobe.com/air/extension/3.4 | AIR 3.4+               | 17              |
| ns.adobe.com/air/extension/3.5 | AIR 3.5+               | 18              |
| ns.adobe.com/air/extension/3.6 | AIR 3.6+               | 19              |
| ns.adobe.com/air/extension/3.7 | AIR 3.7+               | 20              |

> **Note:** The platform options (platform.xml) file requires the
> `ns.adobe.com/air/extension/3.1` namespace or later. If you are using the
> `‑platformoptions` flag to package your ANE, you must specify
> `ns.adobe.com/air/extension/3.1` or later and a SWC version greater than or
> equal to 14. Some platform options file features require later AIR namespace
> and SWF versions.
