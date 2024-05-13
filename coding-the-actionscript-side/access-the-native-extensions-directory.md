# Access the native extension's directory

Sometimes extensions include additional files, such as images. An extension
sometimes also wants to access the information in the extension descriptor file,
such as the extension version number.

To access these files for extensions on all devices except iOS devices, use the
ExtensionContext class static method `getExtensionDirectory()`. For example:

    var extDir:File = ExtensionContext.getExtensionDirectory("com.example.TVControllerExtension");

Pass the name of the extension to `getExtensionDirectory()`. This String value
is the same name you use in:

- the extension descriptor file in the `id` element.

- the extension ID parameter you pass to
  `ExtensionContext.createExtensionContext()`.

The returned File instance refers to the base extension directory. The extension
directory has the following structure:

    extension base directory/
    platform independent files
    META-INF/
        ANE/
            extension.xml
            platform name/
                platform dependent files and directories

Regardless where the extension directory is on the device, the extension's files
are always in the same location relative to the base extension directory.
Therefore, use the returned File instance and File class methods to navigate to
and manipulate specific files included with the extension.

The extension directory location depends on whether the extension is available
through application-bundling or device-bundling as follows:

- With application-bundling, the extension directory is located within the
  application directory.

- With device-bundling, the extension directory location depends on the device.

An exception to using `getExtensionDirectory()` exists for ActionScript
extensions for iOS devices. The resources for these extensions are not located
in the extension directory. Instead, they are located in the top-level
application directory. For more information, see
[Resources on iOS devices](../packaging-a-native-extension/including-resources-in-your-native-extension-package.md#resources-on-ios-devices).

More Help topics

[Extension availability at runtime](../introducing-native-extensions-for-adobe-air/native-extensions-architecture.md#extension-availability-at-runtime)
