# FRENamedFunction

Use the FRENamedFunction to associate an FREFunction that you write with a name.
Use that name in your ActionScript code when calling the native function with
the ExtensionContext instance `call()` method. The structure is defined as
follows:

    typedef struct FRENamedFunction_{
        const uint8_t*        name;
        void*                 functionData;
        FREFunction           function;
    } FRENamedFunction;

The fields of FRENamedFunction have the following meanings:

name  
A const uint8_t\*. This pointer points to a string that the ActionScript side
uses to call the associated C function. That is, the string value is the name
that the ActionScript ExtensionContext `call()` method uses in its
`functionName` parameter. Use UTF-8 encoding for the string and terminate it
with the null character.

functionData  
A void\*. This pointer points to any data you want to associate with this
FREFunction function. When the runtime calls the FREFunction function, it passes
the function this data pointer.

function  
An FRENamedFunction. The function that the runtime associates with the string
given by the `name` field. Define this function with the signature of an
[FREFunction()](../functions-you-implement/frefunction.md).
