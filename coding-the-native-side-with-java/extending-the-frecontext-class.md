# Extending the FREContext class

An [FREContext](../native-c-api-reference/typedefs/frecontext.md) object
provides a set of Java functions and context-specific state. Your extension must
provide at least one concrete implementation of the FREContext class.

The FREContext class defines two abstract methods that you must implement:

- `getFunctions()` — must return a Map object, which the AIR runtime uses to
  look up the functions provided by your context.

- `dispose()` — called by the runtime when the context resources can be cleaned
  up.

#### Disposing a context

The ActionScript side of your extension can call the `dispose()` method of an
ExtensionContext instance. Calling the ActionScript `dispose(`) method causes
the runtime to call the Java `dispose()` method of your FREContext class.

If the ActionScript side does not call `dispose()`, the runtime garbage
collector disposes of the ExtensionContext instance when no more references to
it exist. At that time, the runtime calls the Java `dispose()` method of your
FREContext class.

#### FREContext example

The following example illustrates a simple FREContext implementation. The class
creates a function map containing a single function.

    package com.example;

    import java.util.HashMap;
    import java.util.Map;

    import android.util.Log;

    import com.adobe.fre.FREContext;
    import com.adobe.fre.FREFunction;

    public class ExtensionContext extends FREContext {
        private static final String CTX_NAME = "ExtensionContext";
        private String tag;

        public ExtensionContext( String extensionName ) {
            tag = extensionName + "." + CTX_NAME;
            Log.i(tag, "Creating context");
        }

        @Override
        public void dispose() {
            Log.i(tag, "Dispose context");
        }

        @Override
        public Map<String, FREFunction> getFunctions() {
            Log.i(tag, "Creating function Map");
            Map<String, FREFunction> functionMap = new HashMap<String, FREFunction>();

            functionMap.put( UsefulFunction.KEY, new UsefulFunction() );
            return functionMap;
        }

        public String getIdentifier() {
            return tag;
        }
    }
