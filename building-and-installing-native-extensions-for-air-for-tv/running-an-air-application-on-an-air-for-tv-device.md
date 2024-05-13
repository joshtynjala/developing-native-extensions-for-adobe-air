# Running an AIR application on an AIR for TV device

See
_[Getting Started with Adobe AIR for TV (PDF)](https://web.archive.org/web/20220705161131/http://download.macromedia.com/pub/developer/devices/GettingStartedWithAdobeAIRForTV.pdf)_
for how to install and run an AIR application on an AIR for TV device. Make sure
that you use the following command-line option when you run the stagecraft
binary executable:

    --profile extendedTV

This option is required for the AIR application to be able to use its native
extensions.

When AIR for TV runs the application that contains a stub or simulator
extension, AIR for TV looks for corresponding device-bundled extension on the
device. If it is there, the AIR application uses it. If the device-bundled
extension is not installed on the device, the AIR application uses the stub or
simulator extension.
