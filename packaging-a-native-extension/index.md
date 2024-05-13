# Packaging a native extension

To provide your native extension to application developers, package all the
related files into an ANE file. An AIR application developer uses the ANE file
by:

- Including the ANE file in the application's library path in the same way the
  developer includes a SWC file in the library path. This action allows the
  application to reference the extension's ActionScript classes.

- Packaging the ANE file with the AIR application.

For information on building and packaging an ANE file with an AIR application,
see
[Using native extensions for Adobe AIR](https://web.archive.org/web/20161201093318/http://help.adobe.com/en_US/air/build/WS597e5dadb9cc1e0253f7d2fc1311b491071-8000.html).

Creating a native extension package involves the following tasks:

1.  Build the extension's ActionScript library into a SWC file.

2.  Build the extension's native libraries -- one for each supported target
    platform.

3.  Create a signed certificate for your extension. Signing an extension is
    optional.

4.  Create an extension descriptor file.

5.  Use ADT to create the extension package.

- [Building the ActionScript library of a native extension](./building-the-actionscript-library-of-a-native-extension.md)
- [Creating a signed certificate for a native extension](./creating-a-signed-certificate-for-a-native-extension.md)
- [Creating the extension descriptor file](./creating-the-extension-descriptor-file.md)
- [Building the native library](./building-the-native-library.md)
- [Creating the native extension package](./creating-the-native-extension-package.md)
- [Including resources in your native extension package](./including-resources-in-your-native-extension-package.md)
