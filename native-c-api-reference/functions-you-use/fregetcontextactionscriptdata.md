# FREGetContextActionScriptData()

#### Usage

    FREResult FREGetContextActionScriptData( FREContext ctx, FREObject *actionScriptData);

#### Parameters

ctx  
An FREContext variable. The runtime passed this value to
`FREContextInitializer()`. See
[FREContextInitializer()](../functions-you-implement/frecontextinitializer.md).

actionScriptData  
A pointer to an FREObject variable. When `FREGetContextActionScriptData()` is
successful, the runtime sets this parameter. The value corresponds to the
ActionScript object previously saved with `FRESetContextActionScriptData().`

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded. The `actionScriptData` parameter corresponds to the
ActionScript object previously saved with `FRESetContextActionScriptData().`

FRE_INVALID_ARGUMENT  
The `actionScriptData` parameter is `NULL`.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to get an extension context's ActionScript data.

More Help topics

[FRESetContextActionScriptData()](./fresetcontextactionscriptdata.md)

[Context-specfic data](../../coding-the-native-side-with-c/context-specific-data.md)
