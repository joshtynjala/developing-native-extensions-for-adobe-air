# Working with ActionScript primitive types

In your Java FREFunction implementations, an input parameter can correspond to a
primitive ActionScript type. All parameters passed from ActionScript code to
your extension are of type
[FREObject](../../android-java-api-reference/classes/freobject.md). Therefore,
to work with an ActionScript primitive type input parameter, you get the
ActionScript value of the FREObject parameter. Use the following FREObject
functions:

- `getAsInt()`

- `getAsDouble()`

- `getAsString()`

- `getAsBool()`

If an output parameter or return value of an FREFunction corresponds to a
primitive ActionScript type, you create the ActionScript primitive using a one
of the FREObject factory methods. Use the following static FREObject functions:

- `FREObject.newObject( int value )`

- `FREObject.newObject( double value )`

- `FREObject.newObject( String value )`

- `FREObject.newObject( int boolean )`
