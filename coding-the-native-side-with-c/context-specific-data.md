# Context-specfic data

Context-specific data is specific to an extension context. (Recall that
extension data is for all extension contexts in an extension). The context
initialization method, context finalization method, and native extension methods
can create, access, and modify the context-specific data.

The context-specific data can include the following:

- Native data. This data is any data you choose. It can be a simple primitive
  data type, or a structure you define. See
  [FREGetContextNativeData()](../native-c-api-reference/functions-you-use/fregetcontextnativedata.md)
  and
  [FRESetContextNativeData()](../native-c-api-reference/functions-you-use/fresetcontextnativedata.md).

- ActionScript data. This data is an FREObject variable. Since an FREObject
  variable corresponds to an ActionScript class object, this data allows you to
  save and later access an ActionScript object. See
  [FREGetContextActionScriptData()](../native-c-api-reference/functions-you-use/fregetcontextactionscriptdata.md)
  and
  [FRESetContextActionScriptData()](../native-c-api-reference/functions-you-use/fresetcontextactionscriptdata.md).
  Also see [The FREObject type](./the-freobject-type.md).

A sequence diagram showing the native implementation setting context-specific
native data is in [Extension initialization](./extension-initialization.md). A
sequence diagram showing the native implementation getting the context-specific
data is in [Extension functions](./extension-functions.md).
