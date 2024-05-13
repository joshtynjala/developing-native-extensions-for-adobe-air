# Overview of tasks in developing AIR for TV extensions

When you develop a native extension for an AIR for TV device, do the following
iterative tasks:

1.  Write the native implementation.

    For more information, see
    [Coding the native side with C](../coding-the-native-side-with-c/index.md).

2.  Write the real ActionScript implementation.

    For more information, see
    [Coding the ActionScript side](../coding-the-actionscript-side/index.md). Be
    sure to consider
    [Native extension backward compatibility](../coding-the-actionscript-side/native-extension-backward-compatibility.md).

3.  Write the stub ActionScript implementation, and optionally write a simulator
    ActionScript implementation.

    For more information, see
    [The device-bundled extension and the stub extension](./the-device-bundled-extension-and-the-stub-extension.md)
    and [Check for extension support](./check-for-extension-support.md).

4.  Create a certificate for signing your native extension. This step is
    optional.

    For more information, see
    [Creating a signed certificate for a native extension](../packaging-a-native-extension/creating-a-signed-certificate-for-a-native-extension.md).

5.  Build the device-bundled extension and the stub extension by using the AIR
    for TV make utility. This process creates a ZIP file to install the
    device-bundled extension on the device. It also creates an ANE file of the
    stub extension for an AIR application to build and test with.

    For more information, see
    [Building an AIR for TV native extension](./building-an-air-for-tv-native-extension.md).

6.  If a simulator ActionScript implementation is available, build the simulator
    extension by using the AIR for TV make utility. This process creates an ANE
    file for an AIR application to build and test with.

    For more information, see
    [Building an AIR for TV native extension](./building-an-air-for-tv-native-extension.md).

7.  Add any required resources, such as images, to the ZIP file and ANE file.

    For more information, see
    [Adding resources to your AIR for TV native extension](./adding-resources-to-your-air-for-tv-native-extension.md).

8.  Test the simulator extension on a desktop computer.

    For more information, see
    [Debugging AIR for TV applications](https://web.archive.org/web/20150914222217/http://help.adobe.com/en_US/air/build/WS62b4b4caef5f7931-1f86f0fb1328dba45c2-7fd1.html).

9.  Install the device-bundled extension on the device.

    For more information, see
    [Installing the device-bundled extension on the AIR for TV device](./distributing-your-air-for-tv-native-extension.md#installing-the-device-bundled-extension-on-the-air-for-tv-device).

10. Test the device-bundled extension on the device.

    For more information, see
    [Running an AIR application on an AIR for TV device](./running-an-air-application-on-an-air-for-tv-device.md)
    and
    [Debugging AIR for TV applications](https://web.archive.org/web/20150914222217/http://help.adobe.com/en_US/air/build/WS62b4b4caef5f7931-1f86f0fb1328dba45c2-7fd1.html).

11. Deliver the stub or simulator ANE files, or both, to application developers.
