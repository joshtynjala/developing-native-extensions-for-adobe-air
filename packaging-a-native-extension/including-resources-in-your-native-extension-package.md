# Including resources in your native extension package

The ActionScript side and the native code side of your extension sometimes use
external resources, such as images.

On the ActionScript side, your platform-independent SWC file can include the
resources it requires. If a platform-dependent SWF file requires resources,
include the resources in the platform-dependent directory structure that you
specify in the ADT command.

On the native code side, you can also include resources in the
platform-dependent directory structure. Put the resources in a subdirectory
relative to the native code library, in the location the native code expects.
ADT preserves this directory structure when packaging your ANE.

Using resources on Android and iOS devices have some extra requirements.

## Resources on Android devices

For the `Android-ARM` platform, put the resources in a subdirectory called
`res,` relative to the directory containing the native code library. Populate
the directory with resources as described at
[Providing Resources](https://developer.android.com/guide/topics/resources/providing-resources.html)
on [developer.android.com](https://developer.android.com). When ADT packages the
ANE file, it puts the resources in the `Android-ARM/res` directory of the
resulting ANE package.

When accessing a resource from the extension's Java native code library, use the
`getResourceID()` method in the FREContext class. Do not access the resources
using the standard Android resource ID mechanism. For more information on the
`getResourceID()` method, see
[Method details](../android-java-api-reference/classes/frecontext.md#method-details).

The method `getResourceId()` takes a String parameter that is the resource name.
To avoid resource name conflicts between extensions in an application, provide a
unique name for each resource file in an extension. For example, prefix the
resource name with the extension ID, creating a resource name such as
`com.sample.ext.MyExtension.myImage1.png`.

### Accessing native resources with R.\* mechanism

In previous releases, the native Android resources in the Android Native
Extension could only be accessed by using the `getResourceID()` API while the
R.\* mechanism could not be used with the ANEs. Beginning AIR 4.0, you can
access resources with the R.\* mechanism. When using the R.\* mechanism, ensure
that you use the platform descriptor, platform.xml, which has all the
dependencies defined:

    <?xml version="1.0"?>
    <xs:schema
        xmlns:xs="http://www.w3.org/2001/XMLSchema"
        targetNamespace="http://ns.adobe.com/air/extension/4.0"
        xmlns="http://ns.adobe.com/air/extension/4.0"
        elementFormDefault="qualified">
        <xs:element name="platform">
            <xs:complexType>
                <xs:all>
                    <xs:element name="description"   type="LocalizableType" minOccurs="0"/>
                    <xs:element name="copyright"     type="xs:string"       minOccurs="0"/>
                    <xs:element name="packagedDependencies" minOccurs="0">
                        <xs:complexType>
                            <xs:all>
                                <xs:element name="packagedDependency" type="name" minOccurs="0" maxOccurs="unbounded"/>
                            </xs:all>
                        </xs:complexType>
                    </xs:element>
                    <xs:element name="packagedResources" minOccurs="0">
                        <xs:complexType>
                            <xs:all>
                                <xs:element name="packagedResource" minOccurs="0" maxOccurs="unbounded"/>
                                <xs:complexType>
                                    <xs:all>
                                        <xs:element name="packageName" type="name" minOccurs="0"/>
                                        <xs:element name="folderName" type="name" minOccurs="0"/>
                                    </xs:all>
                                </xs:complexType>
                            </xs:all>
                        </xs:complexType>
                    </xs:element>
                </xs:all>
            </xs:complexType>
        </xs:element>
        <xs:simpleType name="name">
            <xs:restriction base="xs:string">
                <xs:pattern value="[A-Za-z0-9\-\.]{1,255}"/>
            </xs:restriction>
        </xs:simpleType>
        <xs:complexType name="LocalizableType" mixed="true">
            <xs:sequence>
                <xs:element name="text" minOccurs="0" maxOccurs="unbounded">
                    <xs:complexType>
                        <xs:simpleContent>
                            <xs:extension base="xs:string">
                                <xs:attribute name="lang" type="xs:language" use="required"/>
                            </xs:extension>
                        </xs:simpleContent>
                    </xs:complexType>
                </xs:element>
            </xs:sequence>
        </xs:complexType>
    </xs:schema>

Following is an example of the dependencies in `platform.xml`:

    <packagedDependencies>
        <packagedDependency>android-support-v4.jar</packagedDependency>
        <packagedDependency>google-play-services.jar</packagedDependency>
    </packagedDependencies>
    <packagedResources>
        <packagedResource>
            <packageName>com.myane.sampleasextension</packageName>
            <folderName>ane-res</folderName>
        </packagedResource>
        <packagedResource>
            <packageName>com.google.android.gms</packageName>
            <folderName>google-play-services-res</folderName>
        </packagedResource>
    </packagedResources>

where:

- `packagedDependencies` is used to provide the name of all the jars on which
  the ANE is dependent.

- `packagedResources` defines the resources used by the ANE or any other jar
  file.

- `folderName` defines the name of the resources folder.

- `packageName` defines the package name of the jar that uses the resources.

- `packagedDependencies` and `packagedResources` will be available from
  extension namespace 4.0 onwards.

The Android-ARM folder contains all the ANE jar files and resources as well as
the third-party jar files. Following is a sample ANE packaging command:

    bin/adt -package -target ane sample.ane extension.xml -swc sampleane.swc -platform Android-ARM -platformoptions platform.xml -C Android-ARM .

You do not need to merge the third-party jar files and resources with the ANE
jar and resources when using the R.\* resource access mechanism. ADT merges the
jars and resources internally. All dependencies and resources still need to be
packaged in the ANE.

Note that:

- An ANE project should be a library project for the R.\* resource access
  mechanism to work.

- There is no restriction on the name of the resource folder, it can either
  start with 'res' or any other valid string.

- If the `-platformoptions` switch is not used while packaging an ANE, resource
  access is only possible via the `getResourceId()` mechanism.

## Resources on iOS devices

#### Resource location

Before using ADT to create an ANE file for iOS devices, put the non-localized
resources in the directory containing the native code library. Localized
resources go in subdirectories as described in the next section.

However, an iOS application bundle contains its resources at the top level of
the application bundle directory. These resources include all the resources used
by the platform-specific part of each extension. When an AIR application
developer packages an ANE file with the application, ADT does the following:

1.  It looks in the ANE package's `iPhone-ARM` directory.

2.  It considers all files in that directory, except the library.swf and the
    extension descriptor file, as resource files.

3.  It moves the resource files to the top-level directory of the application.

Because resource files from multiple extensions are moved to the same location,
resource filename conflicts are possible. If a conflict exists, ADT does not
package the application and reports the errors. Therefore, provide a unique name
for each resource file in an extension. For example, prefix the name with the
extension ID, creating a resource name such as
`com.sample.ext.MyExtension.myImage1.png`.

> Note: The resources are in the top-level application directory -- not in the
> extension directory. Therefore, to access the resources, use the ActionScript
> property `File.applicationDirectory`. Do not use the ActionScript API
> `ExtensionContext.getExtensionDirectory()` to navigate to the extension
> directory to find the resources. They are not there.

#### Localized resources

Your extension's native code library (but not the ActionScript side) can use
localized resources. To use localized resources, do the following:

- In the platform-specific directory that you specify when creating your ANE
  file using ADT, put the localized resources in language-specific
  subdirectories. Name each of these subdirectories as follows:

      language[_region].lproj

  Set the value of _`language`_ and _`region`_ according to iOS conventions. See
  [Language and Locale Designations](https://web.archive.org/web/20130215190350/http://developer.apple.com/library/ios/#documentation/MacOSX/Conceptual/BPInternational/Articles/LanguageDesignations.html)
  in the iOS Developer Library.

- Put localized strings into .strings files in the format described at
  [String Resources](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/LoadingResources/Strings/Strings.html).
  However, do not name any file `Localizable.strings` because that is the
  default name used in an application bundle.

The following directory structure is an example of a directory that contains all
the iOS platform-specific files to package into the ANE file:

    platform/
                            iOS/
                            library.swf
                            myNativeLibrary.a
                            myNonLocalizedImage1.jpg
                            de.lproj/
                            MyGermanLocalizable.strings
                            MyGermanLocalizedImage1.png
                            en_us.lproj/
                            MyAmericanLocalizable.strings
                            MyAmericanLocalizedImage1.png
                            en_gb.lproj/
                            MyBritishLocalizable.strings
                            MyBritishLocalizedImage1.png
