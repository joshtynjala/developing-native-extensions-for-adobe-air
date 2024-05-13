# Call a native function

After the ActionScript extension class has called
`ExtensionContext.createExtensionContext()`, it can call methods in the native
implementation. The TVChannelController example calls native methods
`"setDeviceChannel"` and `"getDeviceChannel"` as follows:

    package com.example {
    public class TVChannelController extends EventDispatcher {
        private var extContext:ExtensionContext;
        private var channel:int;

        public function TVChannelController() {
            extContext = ExtensionContext.createExtensionContext(
                            "com.example.TVControllerExtension", "channel");
        }

        public function set currentChannel(channelToSet:int):void {
            extContext.call("setDeviceChannel", channelToSet);
        }

        public function get currentChannel():int {
            channel = int (extContext.call("getDeviceChannel"));
            return channel;
        }
    }

The `call()` method of ExtensionContext takes these parameters:

- `functionName`. This string represents a function in the native
  implementation. In the TVChannelController example, these strings are
  different from the ActionScript method names. You can choose to make the names
  the same. You can also choose whether a `functionName` string is the same as
  the name of the native function that it represents. In your native
  implementation, you provide the association between this `functionName` string
  and the native function. The association is in an output parameter of your
  `FREContextInitializer()` method. See
  [Extension context initialization](../coding-the-native-side-with-c/extension-context-initialization.md).

- An optional list of parameters. Each parameter is passed to the native
  function. A parameter can be a primitive type, such as an int, or any
  ActionScript Object.

The return value of the `call()` method of ExtensionContext is a primitive type
or any ActionScript Object. The subclass of Object that it returns depends on
what the native function returns. For example, the native function
`"getDeviceChannel"` returns an int.
