# Coding the native side with Java

Android devices use Java as their primary application development language. If
you are targeting your native extension for such a device, use the native
extensions Java API to code the "native" side of your extension. You can also
use the AIR extension C API with the
[Android Native Development Kit](https://developer.android.com/ndk) for some
purposes. For information on using the C API, see
[Coding the native side with C](../coding-the-native-side-with-c/index.md).

The Java API is provided in the file FlashRuntimeExtensions.jar. The file is
available in the AIR SDK in the `lib/android` directory. The AIR SDK is
available at <https://airsdk.harman.com/>.

To code the Java side of a native extension for Adobe AIR, do the following:

- Implement the
  [FREExtension](../android-java-api-reference/interfaces/freextension.md)
  interface.

- Extend the [FREContext](../android-java-api-reference/classes/frecontext.md)
  abstract class with one or more concrete subclasses.

- Implement the
  [FREFunction](../android-java-api-reference/interfaces/frefunction.md)
  interface for each Java function that can be called from the ActionScript side
  of the extension.

For details about each Java API function, such as parameters and return values,
see [Android Java API Reference](../android-java-api-reference/index.md).

- [Implementing the FREExtension interface](./implementing-the-freextension-interface.md)
- [Extending the FREContext class](./extending-the-frecontext-class.md)
- [Implementing the FREFunction interface](./implementing-the-frefunction-interface.md)
- [Dispatching asynchronous events](./dispatching-asynchronous-events.md)
- [Accessing ActionScript objects](./accessing-actionscript-objects.md)
- [Working with ActionScript primitive types and objects](./working-with-actionscript-primitive-types-and-objects/index.md)
- [Threads and native extensions](./threads-and-native-extensions.md)

## Adobe recommends

> ### ![](../img/oliver_goldman.png) [Adobe TV: How to extend Adobe AIR: mobile](http://goo.gl/IkXfU)
>
> [Oliver Goldman](https://web.archive.org/web/20160229164917/http://blogs.adobe.com/simplicity/)

> ### ![](../img/milkmanGames.png) [Developing Android Extensions for AIR 3: A Beginner's Guide](http://goo.gl/EPSg6)
>
> Milkman Games

> ### ![](../img/adobe_logo.png) [Native extensions for Adobe AIR](https://web.archive.org/web/20160406203944/https://www.adobe.com/devnet/air/native-extensions-for-air.html)
>
> Various Authors
