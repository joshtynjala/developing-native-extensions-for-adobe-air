# FREFunction()

#### Signature

    typedef FREObject (*FREFunction)(
        FREContext             ctx,
        void*            functionData,
        uint32_t             argc,
        FREObject             argv[]
    );

#### Parameters

ctx  
The FREContext variable that represents this extension context. See
[FREContext](../typedefs/frecontext.md).

functionData  
A void\*. This pointer points to the data you associated with this FREFunction
function in its FRENamedFunction structure. Your implementation of
FREContextInitializer() passed a set of FRENamedFunction structures to the
runtime in an out parameter. When the runtime calls the FREFunction function, it
passes the function this data pointer. See
[FRENamedFunction](../structure-typedefs/frenamedfunction.md).

argc  
The number of elements in the `argv` parameter.

argv  
An array of FREObject variables. These pointers correspond to the parameters
passed after the function name in the ActionScript call to the ExtensionContext
instance's `call()` method.

#### Returns

An FREObject variable. The default return value is an FREObject for which the
type is `FRE_INVALID_OBJECT.`

#### Description

Implement a function with the FREFunction signature for each native function in
the extension. The function name corresponds to the `function` field of an
FRENamedFunction element in the array returned in the `functionsToSet` parameter
of the `FREContextInitializer()` function.

The runtime calls this FREFunction function when the ActionScript side calls the
ExtensionContext instance's `call()` method. The first parameter of `call()` is
the same as the `name` field of the FRENamedFunction element. Subsequent
parameters to `call()` correspond to the FREObject variables in the `argv`
array.

You define the FREFunction to return an FREObject variable. The type of the
FREObject variable corresponds to the ActionScript type returned by the `call()`
method. If the FREFunction has no return value, the default return value is an
FREObject variable with the type `FRE_INVALID_OBJECT`. The default return value
results in `call()` returning `null` on the ActionScript side.

Use the `ctx` parameter to:

- Get and set data you associate with the extension. This data can be native
  context data and ActionScript context data. See
  [Context-specfic data](../../coding-the-native-side-with-c/context-specific-data.md).

- Dispatch an asynchronous event to the ExtensionContext instance on the
  ActionScript side. See
  [FREDispatchStatusEventAsync()](../functions-you-use/fredispatchstatuseventasync.md).

Use the functions in [Functions you use](../functions-you-use/index.md) to work
with the FREObject parameters and the return value, if any.

More Help topics

[FREContextInitializer()](./frecontextinitializer.md)

[The FREObject type](../../coding-the-native-side-with-c/the-freobject-type.md)
