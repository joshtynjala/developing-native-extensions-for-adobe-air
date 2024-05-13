# Coding the ActionScript side

A native extension is made of two parts:

- ActionScript extension classes you define.

- A native implementation.

The ActionScript extension classes access and exchange data with the native
implementation. This access is provided with the ActionScript class
ExtensionContext. Only ActionScript code that is part of an extension can access
the ExtensionContext class methods.

Coding the ActionScript side of your extension includes the following tasks:

- Declaring the public interfaces of your ActionScript extension class.

- Using the static method `ExtensionContext.createExtensionContext()` to create
  an ExtensionContext instance.

- Using the `call()` method of the ExtensionContext instance to call methods in
  the native implementation.

- Adding event listeners to the ExtensionContext instance to listen for events
  dispatched from the native implementation.

- Using the `dispose()` method to delete the ExtensionContext instance.

- Sharing data between the ActionScript side and the native side. The data
  shared can be any ActionScript object.

- Using the `getExtensionDirectory()` method to access the directory in which
  the extension is installed. All information and resources related to the
  extension are in this directory. (An exception to this rule exists for iOS
  devices.)

For examples of native extensions, see
[Native extensions for Adobe AIR](https://web.archive.org/web/20160406203944/https://www.adobe.com/devnet/air/native-extensions-for-air.html).

For more information about the ExtensionContext class, see the
_[ActionScript 3.0 Reference for the Adobe Flash Platform](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/index.html)_.

- [Declare the public interfaces](./declare-the-public-interfaces.md)
- [Check for native extension support](./check-for-native-extension-support.md)
- [Create an ExtensionContext instance](./create-an-extensioncontext-instance.md)
- [Call a native function](./call-a-native-function.md)
- [Listen for events](./listen-for-events.md)
- [Dispose of an ExtensionContext instance](./dispose-of-an-extensioncontext-instance.md)
- [Access the native extension's directory](./access-the-native-extensions-directory.md)
- [Identify the calling application from a native extension](./identify-the-calling-application-from-a-native-extension.md)
- [Native extension backward compatibility](./native-extension-backward-compatibility.md)
