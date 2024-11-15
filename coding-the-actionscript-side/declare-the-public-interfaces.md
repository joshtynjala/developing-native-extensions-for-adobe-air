# Declare the public interfaces

The first step in creating a native extension is determining the extension's
public interfaces. Application code uses these public interfaces to interact
with the extension. ActionScript code goes in files with the .as extension.
Create a .as file with your class definition. For example, the following code
shows the declaration of a simple TVChannelController extension class, without
yet filling in its implementation. This simple class allows an application to
manipulate the channel setting on a hypothetical TV.

    package com.example {
        public class TVChannelController extends EventDispatcher {

            public function TVChannelController() {
            }

            public function set currentChannel(channelToSet:int):void {
            }

            public function get currentChannel():int {
            }
        }
    }

> **Note:** When designing your public interfaces, consider whether you will
> release subsequent versions of your extension. If so, consider backward
> compatibility support in your initial design. For more information about
> backward compatibility issues for device-bundled extensions, see
> [Native extension backward compatibility](../coding-the-actionscript-side/native-extension-backward-compatibility.md).
