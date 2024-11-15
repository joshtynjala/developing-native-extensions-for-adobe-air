# Distributing the AIR for TV native extension

## Installing the device-bundled extension on the AIR for TV device

After you have built the device-bundled extension, install it on the device.

The make utility created a ZIP file that contains all the files to install on
the device. Unzip this file onto the device into the following location:

    /opt/adobe/stagecraft/extensions

> **Note:** The /opt/adobe/stagecraft/extensions directory can also be a Linux
> symbolic soft link to another directory on the device filesystem. For more
> information, see the chapter `Filesystem usage` in
> _[Optimizing and Integrating Adobe AIR for TV (PDF)](https://web.archive.org/web/20220705165037/http://download.macromedia.com/pub/developer/devices/OptimizingAndIntegratingAdobeAIRForTV.pdf)_.

## Packaging the stub or simulator extension with an AIR application

For an AIR application to use a device-bundled extension on a device, package
the stub or simulator extension with the AIR application. Use ADT to package the
stub or simulator extension's ANE file with the AIR application to create an
AIRN package file. An AIRN package file is just like a AIR package file, but an
AIRN package file includes an extension ANE file.

For more information, see
_[Packaging an AIR for TV application](https://web.archive.org/web/20150914181852/http://help.adobe.com/en_US/air/build/WS62b4b4caef5f7931-1f86f0fb1328dba45c2-7fd4.html)_.
