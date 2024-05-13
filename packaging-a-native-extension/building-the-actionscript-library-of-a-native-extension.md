# Building the ActionScript library of a native extension

Build the ActionScript side of your extension into a SWC file. The SWC file is
an ActionScript library — an archive file that contains your ActionScript
classes and other resources, such as its images and strings.

When you package a native extension, you need both the SWC file and a separate
library.swf file, which you extract from the SWC file. The SWC file provides the
ActionScript definitions for authoring and compilation. The library.swf provides
the ActionScript implementation used by a specific platform. If different target
platforms of your extension require different ActionScript implementations,
create multiple SWC libraries and extract the library.swf file separately for
each platform. A best practice, however, is that all the ActionScript
implementations have the same public interfaces. (Only one SWC file can be
included in the ANE package.)

The SWC file contains a file called library.swf. For more information, see
[The SWC file and SWF files in the ANE package](./creating-the-native-extension-package.md#the-swc-file-and-swf-files-in-the-ane-package).

Use one of the following ways to build the SWC file:

- Use Adobe Flash Builder to create a Flex library project.

  When you build the Flex library project, Flash Builder creates a SWC file. See
  [Create Flex library projects](https://web.archive.org/web/20150823050554/http://help.adobe.com/en_US/flashbuilder/using/WSe4e4b720da9dedb5-1a92eab212e75b9d8b2-7ffe.html#WSe4e4b720da9dedb5-1a92eab212e75b9d8b2-7ffc).

  Be sure to select the option to include Adobe AIR libraries when you create
  your Flex library project.

  Ensure that the SWC is compiled to the correct version of the SWF format. Use
  SWF 11 for AIR 2.7, SWF 13 for AIR 3, SWF 14 for AIR 3.1, and so on. You can
  set the SWF file format version in the project's properties. Select
  ActionScript Compiler and enter this Additional Compiler Argument:

      -swf-version 17

  > Note: You can use `swfdump` in the Flex SDK bin directory to check the SWF
  > file format version of any SWF file: `swfdump myFlexLibraryProjectSWF.swf`

- Use the command-line tool acompc to build a Flex library project for AIR. This
  tool is the component compiler provided with the Flex SDK. If you are not
  using Flash Builder, use acompc directly. See
  [Using compc, the component compiler](https://web.archive.org/web/20150823050549/http://help.adobe.com/en_US/flex/using/WS2db454920e96a9e51e63e3d11c0bf69084-7fd2.html).

  For example:

      acompc -source-path $HOME/myExtension/actionScript/src
                                  -include-classes sample.extension.MyExtensionClass sample.extension.MyExtensionHelperClass
                                  -swf-version=13
                                  -output $HOME/myExtension/output/sample.extension.myExtension.swc

  > Note: If your ActionScript library uses any external resources, package them
  > into the ANE file using ADT. See
  > [Creating the native extension package](./creating-the-native-extension-package.md).

#### SWF version compatibility

The SWF version specified when compiling the ActionScript library is one of the
factors, along with extension descriptor namespace, that determines whether the
extension is compatible with an AIR application. The SWF version of the
extension cannot exceed the SWF version of the main application SWF file:

|                                    |                 |                                |
| ---------------------------------- | --------------- | ------------------------------ |
| Compatible AIR application version | ANE SWF version | Extension namespace            |
| 3.0+                               | 10-13           | ns.adobe.com/air/extension/2.5 |
| 3.1+                               | 14              | ns.adobe.com/air/extension/3.1 |
| 3.2+                               | 15              | ns.adobe.com/air/extension/3.2 |
| 3.3+                               | 16              | ns.adobe.com/air/extension/3.3 |
| 3.4+                               | 17              | ns.adobe.com/air/extension/3.4 |
| 3.5+                               | 18              | ns.adobe.com/air/extension/3.5 |
| 3.6+                               | 19              | ns.adobe.com/air/extension/3.6 |
| 3.7+                               | 20              | ns.adobe.com/air/extension/3.7 |

> Note: The platform options (platform.xml) file requires the
> `ns.adobe.com/air/extension/3.1` namespace or later. If you are using the
> `‑platformoptions` flag to package your ANE, you must specify
> `ns.adobe.com/air/extension/3.1` or later and a SWC version greater than or
> equal to 14. Some platform options file features require later AIR namespace
> and SWF versions.
