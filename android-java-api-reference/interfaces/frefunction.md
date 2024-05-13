# FREFunction

Package:  
com.adobe.fre

Runtime version  
AIR 3

The FREFunction interface defines the interface used by the runtime to invoke
the Java functions defined in your native extension.

| Method                                               | Description                                                                                        |
| ---------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| FREObject call( FREContext ctx, FREObject\[\] args ) | Called by the AIR runtime when this function is invoked by the ActionScript side of the extension. |

Methods

Implement the FREFunction interface for each Java function in the extension that
can be invoked by the ActionScript portion of the native extension library. Add
the class to the Java Map object returned by the `getFunctions()` method of the
FREContext instance that provides the function.

The runtime invokes the `call()` method when you execute the ExtensionContext
instance's `call()` method in the ActionScript portion.

When you add the FREFunction to the context's function map, you specify a string
value as a key. Use the same value when invoking the function from ActionScript.

## Method details

#### call

    FREObject call( FREContext ctx, FREObject[] args )

Called by the runtime when this function is invoked from ActionScript. Implement
(or initiate) the functionality provided by an FREFunction instance in the
`call()` method.

**Parameters:**

`ctx`  
The FREContext variable that represents this extension context.

Use the `ctx` parameter to:

- Get and set data you associate with the extension context.

- Dispatch an asynchronous event to the ExtensionContext instance on the
  ActionScript side using the FREContext `dispatchStatusEventAsync()` method.

`args`  
The arguments passed to the function as an array of FREObject variables. The
objects in the array are the arguments from the ActionScript ExtensionContext
`call()` method used to invoke the Java function.

**Returns:**

[`FREObject`](../classes/freobject.md)  
The result. All objects shared between the Java and the ActionScript portions of
the extension are encapsulated in an FREObject or one of its subclasses.

## Class Example

The following example illustrates a function that takes a string argument and
returns a new string with the characters reversed. The `call()` function uses
the `ctx` parameter to get an identifier string from the context through which
the function is invoked.

    package com.example;

    import com.adobe.fre.FREContext;
    import com.adobe.fre.FREFunction;
    import com.adobe.fre.FREInvalidObjectException;
    import com.adobe.fre.FREObject;
    import com.adobe.fre.FRETypeMismatchException;
    import com.adobe.fre.FREWrongThreadException;
    import android.util.Log;

    public class ReverseStringFunction implements FREFunction {
        public static final String NAME = "reverseString";
        private String tag;

        public FREObject call(FREContext arg0, FREObject[] arg1) {
            DataExchangeContext ctx = (DataExchangeContext) arg0;
            tag = ctx.getIdentifier() + "." + NAME;
            Log.i( tag, "Invoked " + NAME );
            FREObject returnValue = null;

            try {
                String value = arg1[0].getAsString();
                value = reverse( value );
                returnValue = FREObject.newObject( value );//Invert the received value

            } catch (IllegalStateException e) {
                Log.d(tag, e.getMessage());
                e.printStackTrace();
            } catch (FRETypeMismatchException e) {
                Log.d(tag, e.getMessage());
                e.printStackTrace();
            } catch (FREInvalidObjectException e) {
                Log.d(tag, e.getMessage());
                e.printStackTrace();
            } catch (FREWrongThreadException e) {
                Log.d(tag, e.getMessage());
                e.printStackTrace();
            }

            return returnValue;
        }

        private String reverse( String source ) {
            int i, len = source.length();
            StringBuffer dest = new StringBuffer(len);
            for (i = (len - 1); i >= 0; i--)
                dest.append(source.charAt(i));
            return dest.toString();
        }
    }
