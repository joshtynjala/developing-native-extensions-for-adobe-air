# Implementing the FREExtension interface

Every extension using the Java API must implement the FREExtension interface.
This FREExtension instance is the initial entry point for the Java code in your
extension. Specify the fully qualified name of the class in an `<initializer>`
element in the extension descriptor file. Java implementations can be used for
the Android-ARM platform only. See
[Native extension descriptor files](../native-extension-descriptor-files.md).

The `createContext()` method is the most important part of the
[FREExtension](../android-java-api-reference/interfaces/freextension.md)
implementation. The AIR runtime calls your `createContext()` method when the
ActionScript code of the extension calls
`ExtensionContext.createExtensionContext()`. The method must return an instance
of the FREContext class. The ActionScript `createExtensionContext()` method has
a string parameter which is passed to the Java `createContext()` function. You
can use this value to provide different contexts for different purposes. If your
extension only uses a single context class, you can ignore the parameter.

The other methods of the FREExtension interface, `initialize()` and `dispose(),`
are called by the runtime automatically and can be used to create and clean up
any persistent resources needed by the extension. However, not every extension
needs to do anything in these functions.

The constructor for your FREExtension implementation class must not take any
parameters.

The AIR runtime instantiates your FREExtension instance the first time your
ActionScript code calls `createExtensionContext()`. The sequence of calls to
your Java extension class is:

- FREExtension implementation class constructor

- initialize()

- createContext()

#### FREExtension example

The following example illustrates a simple FREExtension implementation. This
example uses a single extension context. A reference to the context is created
the first time the AIR runtime calls the createContext() method. That reference
is saved for subsequent use.

    package com.example;

    import android.util.Log;

    import com.adobe.fre.FREContext;
    import com.adobe.fre.FREExtension;

    public class Extension implements FREExtension {
        private static final String EXT_NAME = "Extension";
        private ExtensionContext context;
        private String tag = EXT_NAME + "ExtensionClass";

        public FREContext createContext(String arg0) {
            Log.i(tag, "Creating context");
            if( context == null) context = new ExtensionContext(EXT_NAME);
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

#### ExtensionContext example

The following example illustrates the ActionScript code in an extension that
exposes the native extension functionality to application code.

    package com.example
    {
        import flash.external.ExtensionContext;

        public class ExampleExtension
        {
            private const extensionID:String = "com.example.Extension";
            private var extensionContext:ExtensionContext;

            public function ExampleExtension()
            {
                extensionContext = ExtensionContext.createExtensionContext( extensionID, null );
            }

            public function usefulFunction( value:Boolean ):Boolean
            {
                var retValue:Boolean = false;
                retValue = extensionContext.call( "usefulFunctionKey", value );
                return retValue;
            }
        }
    }

#### Application code example

To use a native extension, an application accesses the ActionScript classes and
methods provided by the extension. (In the same way it would access the classes
and methods of any other ActionScript library.)

    var exampleExtension:ExampleExtension = new ExampleExtension();

    var input:Boolean = true;
    var untrue:Boolean = exampleExtension.usefulFunction( input );
