# Listen for events

The native implementation can dispatch events that the ActionScript extension
code can listen for. This mechanism allows the native implementation to perform
tasks asynchronously, notifying the ActionScript side when the task is complete.

The event target is the ExtensionContext instance. Therefore, use the
`addEventListener()` method of the ExtensionContext instance to subscribe to
events from the native implementation.

The following example adds code to TVChannelController to receive an event from
the native implementation. The application using the extension calls the
ActionScript extension class method `scanChannels()`, which in turn calls the
native function `"scanDeviceChannels"`.

This native function asynchronously scans for all available channels. When it
has completed the scan, it dispatches an event. The `onStatus()` method handles
the event by querying the native method `"getDeviceChannels"` for the list of
channels. The `onStatus()` method stores the list in the `scannedChannelList`
data member, and dispatches an event to the application's listening object. When
the application object receives the event, it can call the ActionScript
extension class property accessor `availableChannels`.

    package com.example {
        public class TVChannelController extends EventDispatcher {
            private var extContext:ExtensionContext;
            private var channel:int;
            private var scannedChannelList:Vector.<int>;

            public function TVChannelController() {
                extContext = ExtensionContext.createExtensionContext(
                                "com.example.TVControllerExtension", "channel");
                extContext.addEventListener(StatusEvent.STATUS, onStatus);
            }

            .
            .
            .

            public function scanChannels():void {
                extContext.call("scanDeviceChannels");
            }

            public function get availableChannels():Vector.<int> {
                return scannedChannelList;
            }

            private function onStatus(event:StatusEvent):void {
                if ((event.level == "status") && (event.code == "scanCompleted")) {
                    scannedChannelList = (Vector.<int>)(extContext.call("getDeviceChannels"));
                    dispatchEvent (new Event ("scanCompleted") );
                }
            }
        }
    }

The example illustrates the following points:

- The native implementation can dispatch only a StatusEvent object. Therefore,
  the `addEventListener()` method listens for the event type
  `StatusEvent.STATUS`.

- The native implementation sets the `code` and `level` properties of the
  StatusEvent object. You can define the strings you want to use for these
  properties. In this example, the native implementation sets the `level`
  property to " `status"` and the `code` property to `"scanCompleted"`.
  Typically, the `level` property of a StatusEvent has the value `"status"`,
  `"info"`, or `"error"`.

- Because TVChannelController is a subclass of EventDispatcher, it can also
  dispatch an event. In this example, it dispatches an Event object with the
  `type` property `"scanCompleted"`. Any ActionScript object interested in this
  event can listen for it. For example, the following code shows a snippet from
  an AIR application that uses this extension. The application creates a
  TVChannelController object. Then, it asks the TVChannelController object to
  scan for channels. Then it waits for the scan to complete.

        var channelController:TVChannelController = new TVChannelController();
        channelController.addEventListener("scanCompleted", onChannelsScanned);
        channelController.scanChannels();
        var channelList:Vector.<int>;

        private function onChannelsScanned(evt:Event):void {
            if (evt.type == "scanCompleted") {
                channelList = channelController.availableChannels;
            }
        }
