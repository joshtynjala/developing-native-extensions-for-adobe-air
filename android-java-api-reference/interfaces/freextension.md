# FREExtension

Package:  
com.adobe.fre

Runtime version  
AIR 3

The FREExtension interface defines the interface used by the AIR runtime to
instantiate the Java code in a native extension.

| Method                                                                    | Description                                            |
| ------------------------------------------------------------------------- | ------------------------------------------------------ |
| void initialize()                                                         | Called by the runtime during extension initialization. |
| [FREContext](../classes/frecontext.md) createContext( String contextType) | Creates an FREContext object.                          |
| void dispose()                                                            | Called by the runtime when the extension is destroyed. |

Methods

Every native extension library must implement the FREExtension interface. The
fully qualified name of the implementing class must be present in the
`<initializer>` element of the extension descriptor file.

For example, if the extension Java code is packaged in a JAR file named
_ExampleExtension.jar_ and the class implementing FREExtension is
_com.example.ExampleExtension_ , then you would use the following extension
descriptor entry:

    <platform name="Android-ARM">
        <applicationDeployment>
            <nativeLibrary>ExampleExtension.jar</nativeLibrary>
            <initializer>com.example.ExampleExtension</initializer>
        </applicationDeployment>
    </platform>

The `<finalizer>` element is not needed when using the Java extension interface.

## Method details

#### createContext

    FREContext createContext( String contextType )

Creates an FREContext object.

The AIR runtime calls the Java `createContext()` method after the extension
invokes the ActionScript `ExtensionContext.createExtensionContext()` method. The
runtime uses this context returned for subsequent method invocations.

This function typically uses the `contextType` parameter to choose the set of
methods in the native implementation that the ActionScript side can call. Each
context type corresponds to a different set of methods. Your extension can
create a single context; multiple context instances that provide the same set of
features, but with instance-specific state; or multiple context instances that
provide different features.

**Parameters:**

`contextType`  
A string identifying the type of the context. You define this string as required
by your extension. The context type can indicate any agreed-to meaning between
the ActionScript side and native side of the extension. If your extension has no
use for context types, this value can be `null`. This value is a UTF-8 encoded
string, terminated with the null character.

**Returns:**

[`FREContext`](../classes/frecontext.md)  
the extension context object.

**Example:**

The following example returns a context object based on the `contextType`
parameter. If the `contextType` is the string, "TypeA", the function returns a
unique FREContext instance each time it is called. For other values of
`contextType`, the function only creates a single FREContext instance and stores
it in the private variable `bContext`.

    private FREContext bContext;
    public FREContext createContext( String contextType ) {
        FREContext theContext = null;
        if( contextType == "TypeA" )
        {
            theContext = new TypeAContext();
        }
        else
        {
            if( bContext == null ) bContext = new TypeBContext();
            theContext = bContext;
        }
        return theContext;
    }

#### dispose

    void dispose()

Use the `dispose()` method to clean up any resources created by this
FREExtension implementation. The AIR runtime calls this method when the
associated ActionScript ExtensionContext object is disposed or becomes eligible
for garbage collection.

#### initialize

    void initialize()

Called by the AIR runtime during extension initialization.

## Class Example

The following example illustrates a simple FREExtension example that creates a
single FREContext object. The example also shows how to use the Android Log
class to log informational messages to the Android system log (which you can
view using the `adb logcat` command).

    package com.example;

    import android.util.Log;
    import com.adobe.fre.FREContext;
    import com.adobe.fre.FREExtension;

    public class DataExchangeExtension implements FREExtension {
        private static final String EXT_NAME = "DataExchangeExtension";
        private String tag = EXT_NAME + "ExtensionClass";
        private DataExchangeContext context;

        public FREContext createContext(String arg0) {
            Log.i(tag, "Creating context");
            if( context == null) context = new DataExchangeContext();
            return context;
        }

        public void dispose() {
            Log.i(tag, "Disposing extension");
            // nothing to dispose for this example
        }

        public void initialize() {
            Log.i(tag, "Initialize");
            // nothing to initialize for this example
        }
    }
