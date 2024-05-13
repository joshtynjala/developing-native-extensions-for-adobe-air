# FRESetContextNativeData()

#### Usage

    FREResult FRESetContextNativeData( FREContext ctx, void* nativeData );

#### Parameters

ctx  
An FREContext variable. The runtime passed this value to
`FREContextInitializer()`. See
[FREContextInitializer()](../functions-you-implement/frecontextinitializer.md).

nativeData  
A pointer to the native data.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded.

FRE_INVALID_ARGUMENT  
The `nativeData` parameter is `NULL`.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to set an extension context's native data.

More Help topics

[FREGetContextNativeData()](./fregetcontextnativedata.md)

[Context-specfic data](../../coding-the-native-side-with-c/context-specific-data.md)
