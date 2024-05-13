# Implementing the FREFunction interface

The AIR runtime uses the
[FREFunction](../android-java-api-reference/interfaces/frefunction.md) interface
to invoke your Java functions from ActionScript code. Implement this interface
to expose a concrete piece of functionality.

The FREFunction interface defines a single method, `call()`. This method is
called by the AIR runtime when ActionScript code in the extension invokes the
`call()` method of the ExtensionContext class. To find the right FREFunction
instance, the runtime looks in the FREContext function map. The ActionScript
code passes an array of arguments to the method using the normal ActionScript
types and classes for the arguments. Your Java code sees these values as
FREObject instances. Likewise, your Java `call()` method returns an FREObject
instance and the ActionScript code sees the return value as an ActionScript
type.

When you implement an FREFunction class, you decide on the order of the
parameters in the `call()` method arguments array. Since you also write the
ActionScript side, you use that same parameter order in the ExtensionContext
instance's `call()` method. Therefore, although every Java function parameter is
an FREObject type, you know its corresponding ActionScript type.

Similarly you decide on the ActionScript type of the return value, if any, of a
Java function. The `call()` method returns an object of this type. Although the
Java function return value is always an FREObject instance, you know its
corresponding ActionScript type.

The FREObject instances created by or passed to an FREFunction object have
limited valid life spans. Do not save references to FREObjects between function
invocations.

#### FREFunction example

The following example illustrates a simple FREFunction implementation. The
function takes a boolean parameter and returns its negation.

    package com.example;

    import com.adobe.fre.FREContext;
    import com.adobe.fre.FREFunction;
    import com.adobe.fre.FREObject;

    import android.util.Log;

    public class UsefulFunction implements FREFunction {
        public static final String KEY = "usefulFunctionKey";
        private String tag;

        public FREObject call(FREContext arg0, FREObject[] arg1) {
            ExtensionContext ctx = (ExtensionContext) arg0;
            tag = ctx.getIdentifier() + "." + KEY;
            Log.i( tag, "Invoked " + KEY );
            FREObject returnValue = null;

            try {
                FREObject input = arg1[0];
                Boolean value = input.getAsBool();
                returnValue = FREObject.newObject( !value );//Invert the received value
            } catch (Exception e) {
                Log.d(tag, e.getMessage());
                e.printStackTrace();
            }
            return returnValue;
        }
    }
