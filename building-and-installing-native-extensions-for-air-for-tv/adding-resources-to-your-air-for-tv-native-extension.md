# Adding resources to your AIR for TV native extension

Some AIR for TV native extensions require resources, such as image files. If
your extension uses resources, do the following:

1.  Extract the files from the ZIP file that the make utility created,
    preserving the directory structure.

2.  Add resource directories and files that the extension requires to the
    directory structure.

3.  Rezip the updated directory structure into a ZIP file with the same name as
    the ZIP file that the make utility created.

4.  Extract the files from the ANE file that the make utility created,
    preserving the directory structure. You can use the same tool you use to
    handle ZIP files.

5.  Add resource directories and files that the extension requires to the
    directory structure.

6.  Rezip the updated directory structure into a ZIP file. Rename the file to
    the same name as the ANE file that the make utility created. Make sure that
    you change the filename extension to .ane.

The exact subdirectory structure for your resources within the extension's
directory structure depends on where your extension looks for the resources. The
ActionScript side of the extension can use
`ExtensionContext.getExtensionDirectory()` to locate the extension's directory.
For more information, see
[Access the native extension's directory](../coding-the-actionscript-side/access-the-native-extensions-directory.md).
