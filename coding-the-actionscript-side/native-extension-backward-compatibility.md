# Native extension backward compatibility

## Backward compatibility and the extension's public interfaces

A best practice is to maintain backward compatibility in your extension's
ActionScript public interfaces. Continue to support the extension's classes,
methods, properties, and events in all subsequent versions of the extension.

Device-bundled extensions have a more complex issue with regard to backward
compatibility. Sometimes, the _behavior_ of an extension is different between
versions of an extension. For example, a particular method returns a value with
a new meaning in a new version of the extension. When this behavior occurs for
device-bundled extensions, an application can stop working correctly. This
problem can occur if the application was built with a version of the extension
that behaves differently than the version of the extension installed on the
device. In this case, the application expects one behavior, but the installed
extension provides a different behavior.

In such cases, the extension installed on the device can determine how to
proceed. The extension can do the following:

- Look up the extension version that the AIR application was built with as well
  as the version installed on the device.

- Determine whether the extension's behavior is different in the two versions.

- If the AIR application was built with an older version of the extension,
  revert to the older version's behavior.

  > Note: Typically an AIR application that was built with a newer version of an
  > extension is not available on the device. For more information, see
  > [Backward compatibility and the device's application store](#backward-compatibility-and-the-devices-application-store).

To look up the extension version number that the application was built with, do
the following:

1.  Get the application installation directory using
    `File.applicationDirectory`.

2.  Use the File class APIs to access the extension.xml file of the extension
    that the application built against. The file is at:

        <application directory>/META-INF/AIR/extensions/<extensionID>/META-INF/ANE/extension.xml

3.  Read the contents of the extension.xml file and find the value of the
    `<versionNumber>` element.

To look up the installed extension's version number, do the following:

1.  Use the static method `ExtensionContext.getExtensionDirectory()` to get the
    base directory for the extension.

2.  Use the File class APIs to access the extension.xml file of the extension
    installed on the device. The file is at:

        <extension base directory>/META-INF/ANE/extension.xml

3.  Read the contents of the extension.xml file and find the value of the
    `<versionNumber>` element.

## Backward compatibility and the device's application store

An AIR application that was built with a newer version of the extension than is
installed on the device is typically not available on the device. The
application is not available because of how device manufacturers handle requests
from the device's application store to a server to download such an application.
Adobe recommends the following handling to the device manufacturers:

- Consider the case when the server downloads an application that uses a newer
  version of the extension. The server also downloads the newer version of the
  extension. The device's application store installs both the application and
  the newer version of the extension.

- Consider the case when the server cannot download a newer version of the
  extension. The server also does not download the application that uses that
  version of the extension. The device's application store handles the scenario
  gracefully, informing the end user as needed.

- Consider the case when the server downloads an application that uses a newer
  version of the extension, but does not download the newer version of the
  extension. The device's application store does not allow the end user to run
  the application. The application store handles the scenario gracefully,
  informing the end user as needed.
