# FREObject

Package:  
com.adobe.fre

Inheritance  
java.lang.Object

Subclasses  
[FREArray](./frearray.md), [FREBitmapData](./frebitmapdata.md),
[FREByteArray](./frebytearray.md)

Runtime version  
AIR 3

The FREObject class represents an ActionScript object to Java code.

| Method                                                                                      | Description                                                                                                |
| ------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| public static FREObject newObject( int value)                                               | Creates an FREObject containing a 32-bit signed integer value.                                             |
| public static FREObject newObject( double value)                                            | Creates an FREObject that contains a Java double value, which corresponds to the ActionScript Number type. |
| public static FREObject newObject( boolean value)                                           | Creates an FREObject that contains a boolean value.                                                        |
| public static FREObject newObject( String value)                                            | Creates an FREObject that contains a string value.                                                         |
| public int getAsInt()                                                                       | Accesses the data in the FREObject as a Java int value.                                                    |
| public double getAsDouble()                                                                 | Accesses the data in the FREObject as a Java double value.                                                 |
| public Boolean getAsBool()                                                                  | Accesses the data in the FREObject as a Java boolean value.                                                |
| public String getAsString()                                                                 | Accesses the data in the FREObject as a Java String value.                                                 |
| public static native FREObject newObject( String className, FREObject\[\] constructorArgs ) | Creates an FREObject referencing a new instance of an ActionScript class.                                  |
| public FREObject getProperty( String propertyName )                                         | Gets the value of an ActionScript property.                                                                |
| public void setProperty( String propertyName, FREObject propertyValue )                     | Sets the value of an ActionScript property.                                                                |
| public FREObject callMethod( String methodName, FREObject\[\] methodArgs )                  | Invokes an ActionScript method.                                                                            |

Methods

Use FREObjects to share data between the Java and the ActionScript code in an
extension. The runtime associates an FREObject variable with the corresponding
ActionScript object. You can access the properties and methods of the
ActionScript object associated with an FREObject using the `getProperty()`,
`setProperty()`, and `callMethod()` functions.

An FREObject is a general purpose object. It can represent a primitive value or
a class type. If you access the object in a way that is incompatible with the
data in the object, an FRETypeMismatchException is thrown.

FREObjects can be used to represent any ActionScript object. In addition, the
subclasses FREArray, FREBitmapData, and FREByteArray provide additional methods
for handling specific kinds of data.

You can pass data from Java to ActionScript code by returning an FREObject from
the `call()` method of an [FREFunction](../interfaces/frefunction.md) instance.
The ActionScript code receives the data as an ActionScript Object, which can be
cast to the appropriate primitive or class type. You can also set the properties
and call the methods of an ActionScript object for which you have an FREObject
reference. When setting a property or the parameter of an ActionScript method,
you use an FREObject.

You can pass data from ActionScript to Java code as the parameter to the
`call()` method of an FREFunction instance. The argument is encapsulated in an
FREObject instance when the `call()` method is invoked. If the argument is a
reference to an ActionScript object, the Java code can read the property values
and call the methods of that object. These properties and function return values
are provided to your Java code as FREObjects. You can use the FREObject methods
to access the data as Java types and, when appropriate, downcast the object to
an FREObject subclass such as FREBitmapData.

## Method details

#### newObject( int )

    public static FREObject newObject( int value )

Creates an FREObject containing a 32-bit signed integer value.

**Parameters:**

`value`  
A signed integer.

**Returns:**

`FREObject`  
An FREObject.

**Example:**

    FREObject value = FREObject.newObject( 4 );

#### newObject( double )

    public static FREObject newObject( double value )

Creates an FREObject that contains a Java double value, which corresponds to the
ActionScript Number type.

**Parameters:**

`value`  
A double.

**Returns:**

`FREObject`  
An FREObject.

**Example:**

    FREObject value = FREObject.newObject( 3.14156d );

#### newObject( boolean )

    public static FREObject newObject( boolean value )

Creates an FREObject that contains a boolean value.

**Parameters:**

`value`  
true or false.

**Returns:**

`FREObject`  
An FREObject.

**Example:**

    FREObject value = FREObject.newObject( true );

#### newObject( String )

    public static FREObject newObject( String value )

Creates an FREObject that contains a string value.

**Parameters:**

`value`  
A string.

**Returns:**

`FREObject`  
An FREObject.

**Example:**

    FREObject value = FREObject.newObject( "A string value" );

#### getAsInt

    public int getAsInt()

Accesses the data in the FREObject as a Java int value.

**Returns:**

`int`  
The integer value.

**Example:**

    int value = FREObject.getAsInt();

#### getAsDouble

    public double getAsDouble()

Accesses the data in the FREObject as a Java double value.

**Returns:**

`double`  
The double value.

**Example:**

    double value = FREObject.getAsInt();

#### getAsBool

    public Boolean getAsBool()

Accesses the data in the FREObject as a Java boolean value.

**Returns:**

`boolean`  
`true` or `false`

**Example:**

    boolean value = FREObject.getAsInt();

#### getAsString

    public String getAsString()

Accesses the data in the FREObject as a Java String value.

**Returns:**

`String`  
The string value.

**Example:**

    String value = FREObject.getAsInt();

#### newObject( String, FREObject\[\] )

    public static native FREObject newObject( String className, FREObject[] constructorArgs )

Creates an FREObject referencing a new instance of an ActionScript class.

**Parameters:**

`className`  
The fully-qualified ActionScript class name.

`constructorArgs`  
The arguments to pass to the ActionScript class constructor as an array of
FREObjects. Set to `null` if the class constructor has no parameters.

**Returns:**

`FREObject`  
An FREObject representing a new instance of an ActionScript class.

**Example:**

    FREObject matrix = FREObject.newObject( "flash.geom.Matrix", null );

#### getProperty

    public FREObject getProperty( String propertyName )

Gets the value of an ActionScript property.

**Parameters:**

`propertyName`  
The name of the property to access.

**Returns:**

`FREObject`  
The value of the specified property as an FREObject.

**Example:**

    FREObject isDir = fileobject.getProperty( "isDirectory" );

#### setProperty

    public void setProperty( String propertyName, FREObject propertyValue )

Sets the value of an ActionScript property.

**Parameters:**

`propertyName`  
The name of the property to set.

`propertyValue`  
An FREObject containing the new property value.

**Example:**

    fileobject.setProperty( "url", FREObject.newObject( "app://file.txt" ) );

#### callMethod

    public FREObject callMethod( String methodName, FREObject[] methodArgs )

Invokes an ActionScript method.

**Parameters:**

`methodName`  
The name of the method to invoke.

`methodArgs`  
An array of FREObjects containing the arguments for the method in the order in
which the method parameters are declared.

**Returns:**

`FREObject`  
The method result. If the ActionScript method returns an Array, Vector, or
BitmapData object, you can cast the result to an appropriate subclass of
FREObject.

**Example:**

    FREObject[] args = new FREObject[1]
    args[0] = FREObject.newObject( "assets/image.jpg" );
    FREObject imageFile = directoryobject.callMethod( "resolvePath", args );
