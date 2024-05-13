# FRESetArrayLength()

#### Usage

    FREResult FRESetArrayLength (
            FREObject             arrayOrVector,
            uint32_t             length
    );

#### Parameters

arrayOrVector  
An FREObject that represents an ActionScript Array or Vector class object.

length  
A uint32_t. This method sets the length of the Array or Vector class object to
this parameter's value.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded. The runtime has changed the size of the Array or Vector
object.

FRE_ILLEGAL_STATE  
The extension context has acquired an ActionScript BitmapData or ByteArray
object. The context cannot call this method until it releases the BitmapData or
ByteArray object.

FRE_INSUFFICIENT_MEMORY  
The runtime could not allocate enough memory to change the size of the Array or
Vector object.

FRE_INVALID_ARGUMENT  
The `length` parameter is greater than 2 <sup>32</sup> .

FRE_INVALID_OBJECT  
The `arrayOrVector` FREObject parameter is invalid.

FRE_READ_ONLY  
The `arrayOrVector` FREObject parameter represents a ActionScript Vector object
that has a fixed size. (Its `fixed` property is true.)

FRE_TYPE_MISMATCH  
The `arrayOrVector` FREObject parameter does not represent an ActionScript Array
or Vector class object.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to set the length of an ActionScript Array or Vector class
object. The FREObject parameter `arrayOrVector` corresponds to the Array or
Vector object. The runtime changes the size of the Array or Vector object as
specified by the `length` parameter.

More Help topics

[FREGetArrayElementAt()](./fregetarrayelementat.md)

[FREGetArrayLength()](./fregetarraylength.md)
