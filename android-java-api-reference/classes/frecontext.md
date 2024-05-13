# FREContext

Package:  
com.adobe.fre

Inheritance  
java.lang.Object

Runtime version  
AIR 3

The FREContext class represents a Java execution context defined by an AIR
native extension.

| Method                                                            | Description                                                                                                                   |
| ----------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| public abstract Map\<String,FREFunction\> getFunctions()          | Called by the AIR runtime to discover the functions provided by this context.                                                 |
| public FREObject getActionScriptData()                            | Gets any data in the `actionScriptData` property of the ActionScript ExtensionContext object associated with this FREContext. |
| public void setActionScriptData( FREObject )                      | Sets the `actionScriptData` property of the ActionScript ExtensionContext object associated with this FREContext.             |
| public abstract void dispose()                                    | Called by the AIR runtime when the ActionScript ExtensionContext object associated with this FREContext instance is disposed. |
| public android.app.Activity getActivity()                         | Returns the application Activity.                                                                                             |
| public native int getResourceId( String resourceString )          | Returns the ID for an Android resource.                                                                                       |
| public void dispatchStatusEventAsync( String code, String level ) | Dispatches a StatusEvent to the application via the ExtensionContext object associated with this FREContext instance.         |

Methods

Your extension must define one or more concrete subclasses of the FREContext
class. The `createContext()` method in your implementation of the
[FREExtension](../interfaces/freextension.md) class creates instances of these
classes when the ActionScript side of the extension invokes the
`ExtensionContext.createExtensionContext()` method.

You can organize the contexts provided by an extension in various ways. For
example, you could create a single instance of a context class that persists for
the lifetime of the application. Alternately, you could create a context class
that is closely bound to a set of native objects with limited lifespan. You
could then create a separate context instance for each set of these objects and
dispose the context instance along with the associated native objects.

> Note: If you have called the acquire() method of any FREByteArray or
> FREBitmapData object, then you cannot call the methods defined by the
> FREObject class of any object.

## Method details

#### getFunctions

    public abstract Map<String,FREFunction> getFunctions()

Implement this function to return a Java Map instance that contains all the
functions exposed by the context. The map key value is used to look up the
FREFunction object when a function is invoked.

**Returns:**

`Map<String, FREFunction>`  
A Map object containing a string key value and a corresponding FREFunction
object. The AIR runtime uses this Map object to look up the function to invoke
when the ActionScript part of the extension invokes the `call()` method of the
ExtensionContext class.

**Example:**

The following getFunctions() example creates a Java HashMap containing three
hypothetical functions. You can invoke these functions in the ActionScript code
of the extension by passing the string, "negate", "invert", or "reverse" to the
ExtensionContext `call()` method.

    @Override
    public Map<String, FREFunction> getFunctions() {
        Map<String, FREFunction> functionMap = new HashMap<String, FREFunction>();
        functionMap.put( "negate", new NegateFunction() );
        functionMap.put( "invert", new InvertFunction() );
        functionMap.put( "reverse", new ReverseFunction() );
        return functionMap;
    }

#### getActionScriptData

    public FREObject getActionScriptData()

Gets the ActionScript data object associated with this context. This data object
can be read and modified by both Java and ActionScript code.

**Returns:**

`FREObject`  
An FREObject representing the data object.

**Example:**

    FREObject data = context.getActionScriptData();

#### setActionScriptData

public void setActionScriptData( FREObject object )

Sets the ActionScript data object associated with this context. This data object
can be read and modified by both Java and ActionScript code.

**Parameters:**

`value`  
An FREObject containing a primitive value or an ActionScript object.

**Example:**

    FREObject data = FREObject.newObject( "A string" );
    context.setActionScriptData( data );

#### getActivity

    public android.app.Activity getActivity()

Gets a reference to the application Activity object. This reference is required
by many APIs in the Android SDK.

**Returns:**

`android.app.Activity`  
The Activity object of the AIR application.

**Example:**

    Activity activity = context.getActivity();

#### getResourceID

    public native int getResourceId( String resourceString )

Looks up the resource ID of a native Android resource.

Specify the string identifying the resource in the `resourceString` parameter.
Follows the naming conventions for resource access on Android. For example a
resource that you would access in Android native code as:

    R.string.my_string

would have the following `resourceString`:

    "string.my_string"

This method will throw Resources.NotFoundException if the resource specified by
`resourceString` cannot be found.

**Parameters:**

`resourceString`  
A string identifying the Android resource.

**Returns:**

`int`  
The ID of the Android resource.

**Example:**

    int myResourceID = context.getResourceID( "string.my_string" );

#### dispatchStatusEventAsync

    public void dispatchStatusEventAsync( String code, String level )

Call this function to dispatch an ActionScript StatusEvent event. The target of
the event is the ActionScript ExtensionContext instance that the runtime
associated with this FREContext object.

Typically, the events this function dispatches are asynchronous. For example, an
extension method can start another thread to perform some task. When the task in
the other thread completes, that thread calls `dispatchStatusEventAsync()` to
inform the ActionScript ExtensionContext instance.

> Note: The `dispatchStatusEventAsync()` function is the only Java API that you
> can call from any thread of your native implementation.

The runtime does not dispatch the event in the following cases:

- The runtime has already disposed of the ExtensionContext instance.

- The runtime is in the process of disposing of the ExtensionContext instance.

- The ExtensionContext instance has no references. It is eligible for the
  runtime garbage collector to dispose of it.

Set the `code` and `level` parameters to any string values. These values can be
anything you want, but coordinate them with the ActionScript side of the
extension.

**Parameters:**

`code`  
A description of the status being reported.

`level`  
The extension-defined category of message.

**Example:**

    context.dispatchStatusEventAsync( "Processing finished", "progress" );

#### dispose

    public abstract void dispose()

Called by the AIR runtime when an associated ActionScript ExtensionContext
object is disposed and this FREContext object has no other references. You can
implement this method to clean up context resources.

## Class Example

The following example creates a subclass of FREContext to return context
information:

    package com.example;

    import java.util.HashMap;
    import java.util.Map;
    import android.util.Log;
    import com.adobe.fre.FREContext;
    import com.adobe.fre.FREFunction;

    public class DataExchangeContext extends FREContext {
        private static final String CTX_NAME = "DataExchangeContext";
        private String tag;

        public DataExchangeContext( String extensionName ) {
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
            functionMap.put( NegateBooleanFunction.NAME, new NegateBooleanFunction() );
            functionMap.put( InvertBitmapDataFunction.NAME, new InvertBitmapDataFunction() );
            functionMap.put( InvertByteArrayFunction.NAME, new InvertByteArrayFunction() );
            functionMap.put( InvertNumberFunction.NAME, new InvertNumberFunction() );
            functionMap.put( ReverseArrayFunction.NAME, new ReverseArrayFunction() );
            functionMap.put( ReverseStringFunction.NAME, new ReverseStringFunction() );
            functionMap.put( ReverseVectorFunction.NAME, new ReverseVectorFunction() );

            return functionMap;
        }

        public String getIdentifier()
        {
            return tag;
        }
    }
