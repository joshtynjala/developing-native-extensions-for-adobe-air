# Identify the calling application from a native extension

The ActionScript side of your extension can identify and evaluate the AIR
application using the extension. For example, use the ActionScript class
[NativeApplication](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/desktop/NativeApplication.html)
to get information about the AIR application, such as its ID and signature data.
Then the ActionScript side can make runtime decisions based on this information.

Sometimes the native implementation has similar runtime decisions to make. In
this case, the ActionScript side can use the `call()` method of an
ExtensionContext instance to report the application information to the native
implementation.
