# Native extension descriptor files

An extension descriptor file describes the contents of a native extension
package.

#### Example extension descriptor

The following extension descriptor document describes a native extension for:

- an Android device

- a _default_ ActionScript implementation for other platforms

    <extension xmlns="http://ns.adobe.com/air/extension/3.1">
        <id>com.example.MyExtension</id>
        <versionNumber>0.0.1</versionNumber>
        <platforms>
            <platform name="Android-ARM">
                <applicationDeployment>
                    <nativeLibrary>MyExtension.jar</nativeLibrary>
                    <initializer>com.sample.ext.MyExtension</initializer>
                </applicationDeployment>
            <platform name="default">
                <applicationDeployment/>
            </platform>
        </platforms>
    </extension>

## The extension descriptor file structure

The extension descriptor file is an XML document with the following structure:

    <extension xmlns="http://ns.adobe.com/air/extension/2.5">
        <id>...</id>
        <versionNumber>...</versionNumber>
        <name>
            <text xml:lang="language_code">...</text>
        </name>
        <description>
            <text xml:lang="language_code">...</text>
        </description>
        <platforms>
            <platform name="device">
                <applicationDeployment>
                    <nativeLibrary>...</nativeLibrary>
                    <initializer>...</initializer>
                    <finalizer>...</finalizer>
                </applicationDeployment>
            </platform>
            <platform name="device">
                <deviceDeployment/>
            </platform>
            <platform name="default">
                <applicationDeployment/>
            </platform>
        </platforms>
    </extension>

## Native extension descriptor elements

The following dictionary of elements describes each of the legal elements of an
AIR application descriptor file.

### applicationDeployment

Declares a native code library included in the extension package and, hence,
deployed with the application.

Each `platform` element must contain either the `applicationDeployment` element
or the `deviceDeployment` element, but not both.

**Parent elements:**

[platform](#platform).

**Child elements:**

- [finalizer](#finalizer)

- [initializer](#initializer)

- [nativeLibrary](#nativelibrary)

#### Content

Identifies the native code library and the initialization and finalization
functions. When the platform name is `default`, the `applicationDeployment`
element has no child elements because the `default` platform has no native code
libraries.

#### Example

    <applicationDeployment>
        <nativeLibrary>myExtension.so</nativeLibrary>
        <initializer>com.example.extension.Initializer</initializer>
        <finalizer>com.example.extension.Finalizer</finalizer>
    </applicationDeployment>

### copyright

A copyright declaration for the extension.

**Parent elements:**

[extension](#extension)

**Child elements:**

none

#### Content

A string containing copyright information.

#### Example

    <copyright>© 2010, Examples, Inc. All rights reserved.</copyright>

### description

The description of the extension.

**Parent elements:**

[extension](#extension)

**Child elements:**

[text](#text)

#### Content

Use a simple text node or multiple `text` elements.

Using multiple `text` elements, you can specify multiple languages in the
`description` element. The `xml:lang` attribute for each text element specifies
a language code, as defined in [RFC4646](https://www.ietf.org/rfc/rfc4646.txt).

#### Example

Description with simple text node:

    <description>This is a sample native extension for Adobe AIR.</description>

Description with localized text elements for English, French, and Spanish:

    <description>
        <text xml:lang="en">This is a example.</text>
        <text xml:lang="fr">C'est un exemple.</text>
        <text xml:lang="es">Esto es un ejemplo.</text>
    </description>

### deviceDeployment

Declares a native extension for which the code libraries are deployed separately
on the device and are not included in this extension package.

Device deployment is not supported by all platforms.

Each `platform` element must contain either the `applicationDeployment` element
or the `deviceDeployment` element, but not both.

**Parent elements:**

[platform](#platform)

**Child elements:**

None.

#### Content

None. The `deviceDeployment` element must be empty.

#### Example

    <deviceDeployment/>

### extension

The root element of the extension descriptor document.

**Parent elements:**

None.

**Child elements:**

- [copyright](#copyright)

- [description](#description)

- [id](#id)

- [name](#name)

- [platforms](#platforms)

- [versionNumber](#versionnumber)

#### Content

Identifies the supported platforms and the code libraries for each platform.

The `extension` element contains a namespace attribute called `xmlns`. Set the
`xmlns` value to one of the following values:

    xmlns="http://ns.adobe.com/air/extension/3.1"
    xmlns="http://ns.adobe.com/air/extension/2.5"

The namespace is one of the factors, along with the SWF version, that determines
compatibility between an AIR SDK and an ANE file. The AIR application must be
packaged with a version of the AIR SDK that equals or exceeds the extension
namespace. Thus an AIR 3 application can use an extension with the 2.5
namespace, but not the 3.1 namespace.

#### Example

    <extension xmlns="http://ns.adobe.com/air/extension/2.5">
        <id>com.example.MyExtension</id>
        <versionNumber>1.0.1</versionNumber>
        <platforms>
            <platform name="Polyphonic-MIPS">
                <deviceDeployment/>
            </platform>
            <platform name="NeoTech-ARM">
                <deviceDeployment/>
            </platform>
            <platform name="Philsung-x86">
                <deviceDeployment/>
            </platform>
            <platform name="default">
                <applicationDeployment/>
            </platform>
        </platforms>
    </extension>

### finalizer

The finalization function defined in the native library.

**Parent elements:**

[applicationDeployment](#applicationdeployment)

**Child elements:**

None.

#### Content

The name of the finalizer function if the extension uses the C API in its native
library.

If the extension uses the Java API, this element contains the name of the class
that implements the FREExtension interface.

The value can contain these characters: A - Z, a - z, 0 - 9, period (.), and
dash (-).

#### Example

    <finalizer>...</finalizer>

### id

The ID of the extension.

**Parent elements:**

[extension](#extension)

**Child elements:**

None.

#### Content

Specifies the ID of the extension.

The value can contain these characters: A - Z, a - z, 0 - 9, period (.), and
dash (-).

#### Example

    <id>com.example.MyExtension</id>

### initializer

The initialization function defined in the native library. An initializer
element is required if the `nativeLibrary` element is used.

**Parent elements:**

[applicationDeployment](#applicationdeployment)

**Child elements:**

None.

#### Content

The name of the initialization function if the extension uses the C API in its
native library.

If the extension uses the Java API, this element contains the name of the class
that implements the FREExtension interface.

The value can contain these characters: A - Z, a - z, 0 - 9, period (.), and
dash (-).

#### Example

    <initializer>...</initializer>

### name

The name of the extension.

**Parent elements:**

[extension](#extension)

**Child elements:**

[text](#text)

#### Content

If you specify a single text node (instead of multiple `<text>` elements), the
AIR application installer uses this name, regardless of the system language.

The `xml:lang` attribute for each text element specifies a language code, as
defined in [RFC4646](https://www.ietf.org/rfc/rfc4646.txt).

#### Example

The following example defines a name with a simple text node:

    <name>Test Extension</name>

The following example, specifies the name in three languages (English, French,
and Spanish) using \<text\> element nodes:

    <name>
        <text xml:lang="en">Hello AIR</text>
        <text xml:lang="fr">Bonjour AIR</text>
        <text xml:lang="es">Hola AIR</text>
    </name>

### nativeLibrary

The native library file included in the extension package for a platform.
Consider the following:

- The `nativeLibrary` element is not required if the extension contains only
  ActionScript code.

- If the `nativeLibrary` element is not used, the `initializer` and `finalizer`
  elements cannot be used either.

- If the `nativeLibrary` element is used, the `initializer` element is also
  required.

**Parent elements:**

[applicationDeployment](#applicationdeployment)

**Child elements:**

None.

#### Content

The filename of the native library included in the extension package.

The value can contain these characters: A - Z, a - z, 0 - 9, period (.), and
dash (-).

#### Example

    <nativeLibrary>extensioncode.so</nativeLibrary>

### platform

Specifies the native code library for the extension on a specific platform.

**Parent elements:**

[platforms](#platforms)

**Child elements:**

One, and only one, of the following elements:

- [applicationDeployment](#applicationdeployment)

- [deviceDeployment](#devicedeployment)

#### Content

The `name` attribute specifies the name of the platform. The special `default`
platform name allows the extension developer to include an ActionScript library
that simulates the behavior of the native code on unsupported platforms.
Simulated behavior can be used to support debugging and to provide fall back
behavior for multi-platform applications.

Use the following values for the `name` attribute:

- `Android-ARM` for Android devices.

- `default`

- `iPhone-ARM` for iOS devices.

- `iPhone-x86` for the iOS Simulator.

- `MacOS-x86-64` for Mac OS X devices.

- `QNX-ARM` for Blackberry Tablet OS devices.

- `Windows-x86` for Windows devices.

- `appleTV-ARM` for tvOS devices.

- `appleTV-x86` for the tvOS Simulator.

> Note: Device-bundled extensions use a `name` attribute value defined by the
> device manufacturer.

The child elements specify how the native code library is deployed. Application
deployment means that the code library is deployed with each AIR application
that uses it. The code library must be included in the extension package. Device
deployment means that the code library is deployed separately to the platform
and is not included in the extension package. The two deployment types are
mutually exclusive; include only one deployment element.

#### Example

    <platform name="Philsung-x86">
        <deviceDeployment/>
    </platform>
    <platform name="default">
        <applicationDeployment/>
    </platform>

### platforms

Specifies the platforms supported by this extension.

**Parent elements:**

[extension](#extension)

**Child elements:**

[platform](#platform)

#### Content

A `platform` element for each supported platform. Optionally, a special
_default_ platform can be specified containing an ActionScript implementation
for use on platforms not supported with a specific code library.

#### Example

    <platforms>
        <platform name="Android-ARM">
            <applicationDeployment>
                <nativeLibrary>MyExtension.jar</nativeLibrary>
                <initializer>com.sample.ext.MyExtension</initializer>
                <finalizer>com.sample.ext.MyExtension</finalizer>
            </applicationDeployment>
        </platform>
        <platform name="iPhone-ARM">
            <applicationDeployment>
                <nativeLibrary>MyExtension.a</nativeLibrary>
                <initializer>InitMyExtension></initializer>
            </applicationDeployment>
        </platform>
        <platform name="Philsung-x86">
            <deviceDeployment/>
        </platform>
        <platform name="default">
            <applicationDeployment/>
        </platform>
        <platform name="appleTV-ARM">
            <applicationDeployment>
                <nativeLibrary>MyExtension.a</nativeLibrary>
                <initializer>InitMyExtension></initializer>
            </applicationDeployment>
        </platform>
    </platforms>

### text

Specifies a localized string.

The `xml:lang` attribute of a text element specifies a language code, as defined
in [RFC4646](https://www.ietf.org/rfc/rfc4646.txt).

AIR uses the `text` element with the `xml:lang` attribute value that most
closely matches the user interface language of the user's operating system.

For example, consider an installation in which a `text` element includes a value
for the en (English) locale. AIR uses the en name if the operating system
identifies en (English) as the user interface language. It also uses the en name
if the system user interface language is en-US (U.S. English). However, if the
user interface language is en-US and the application descriptor file defines
both en-US and en-GB names, then the AIR application installer uses the en-US
value.

If the application defines no `text` element that matches the system user
interface languages, AIR uses the first `name` value defined in the extension
descriptor file.

**Parent elements:**

- [name](#name)

- [description](#description)

**Child elements:**

none

#### Content

An `xml:lang` attribute specifying a locale and a string of localized text.

#### Example

    <text xml:lang="fr">Bonjour AIR</text>

### versionNumber

The extension version number.

**Parent elements:**

[extension](#extension)

**Child elements:**

none

#### Content

The version number can contain a sequence of up to three integers separated by
periods. Each integer must be a number from 0 to 999 (inclusive).

#### Examples

    <versionNumber>1.0.657</versionNumber>

    <versionNumber>10</versionNumber>

    <versionNumber>0.01</versionNumber>
