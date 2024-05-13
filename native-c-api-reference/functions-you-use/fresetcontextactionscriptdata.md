# FRESetContextActionScriptData()

#### Usage

    FREResult FRESetContextActionScriptData( FREContext ctx, FREObject actionScriptData);

#### Parameters

ctx  
An FREContext variable. The runtime passed this value to
`FREContextInitializer()`. See
[FREContextInitializer()](../functions-you-implement/frecontextinitializer.md).

actionScriptData  
An FREObject variable.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded.

FRE_INVALID_OBJECT  
The `actionScriptData` parameter is an invalid FREObject variable.

FRE_INVALID_ARGUMENT  
An argument is invalid.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to set an extension context's ActionScript data.

More Help topics

[FREGetContextActionScriptData()](./fregetcontextactionscriptdata.md)

[Context-specfic data](../../coding-the-native-side-with-c/context-specific-data.md)
