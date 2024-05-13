# Coding the native side with C

Some devices use the C programming language in their native implementations. If
you are targeting your native extension for such a device, use the native
extensions C API to code the native side of your extension.

The C API is in the file FlashRuntimeExtensions.h. The file is available in the
AIR SDK in the `include` directory. The AIR SDK is available at
<https://airsdk.harman.com/>.

The AIR runtime connects the ActionScript side of an extension to the native
side of the extension.

Using the C API, you do the following tasks:

- Initialize the extension.

- Initialize each extension context when it is created.

- Define functions that the ActionScript side can call.

- Dispatch events to the ActionScript side.

- Access data passed from the ActionScript side, and pass data back to the
  ActionScript side.

- Create and access context-specific native data and context-specific
  ActionScript data.

- Clean up extension resources when the extension's work is done.

For details about each C API function, such as parameters and return values, see
[Native C API Reference](../native-c-api-reference/index.md).

For examples of native extensions that use the C API, see
[Native extensions for Adobe AIR](https://web.archive.org/web/20160406203944/https://www.adobe.com/devnet/air/native-extensions-for-air.html).

- [Extension initialization](./extension-initialization.md)
- [Extension context initialization](./extension-context-initialization.md)
- [Context-specfic data](./context-specific-data.md)
- [Extension context finalization](./extension-context-finalization.md)
- [Extension finalization](./extension-finalization.md)
- [Extension functions](./extension-functions.md)
- [Dispatching asynchronous events](./dispatching-asynchronous-events.md)
- [The FREObject type](./the-freobject-type.md)
- [Working with ActionScript primitive types and objects](./working-with-actionscript-primitive-types-and-objects/)
- [Threads and native extensions](./threads-and-native-extensions.md)

## Adobe recommends

> ### ![](../img/oliver_goldman.png) [Adobe TV: How to extend Adobe AIR: mobile](http://goo.gl/IkXfU)
>
> [Oliver Goldman](https://web.archive.org/web/20160229164917/http://blogs.adobe.com/simplicity/)

> ### ![](../img/anthony_mccormick.png) [Native Extensions for AIR and iOS](http://goo.gl/vav8g)
>
> Anthony McCormick: Liquid Photos

> ### ![](../img/nick_kwiatkowski.png) [Creating a Windows AIR Native Extension with Eclipse](http://goo.gl/1EFu2)
>
> [Nick Kwiatkowski: QueTwo](https://web.archive.org/web/20160315023414/http://quetwo.com/)

> ### ![](../img/adobe_logo.png) <a href="https://web.archive.org/web/20160406203944/https://www.adobe.com/devnet/air/native-extensions-for-air.html">Native extensions for Adobe AIR</a>
>
> Various Authors
