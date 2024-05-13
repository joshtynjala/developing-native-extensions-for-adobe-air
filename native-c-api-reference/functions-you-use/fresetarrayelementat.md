# FRESetArrayElementAt()

#### Usage

    FREResult FRESetArrayElementAt (
            FREObject             arrayOrVector,
            uint32_t             index,
            FREObject             value
    );

#### Parameters

arrayOrVector  
An FREObject that points to data that represents an ActionScript Array or Vector
class object.

index  
A uint32_t that contains the index of the Array or Vector element to set. The
first element of an Array or Vector object has index 0.

value  
An FREObject. This method sets the Array or Vector element specified by `index`
to the ActionScript object represented by the FREObject `value` parameter.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded. The Array or Vector element is set to the `value`
FREOjbect parameter.

FRE_ILLEGAL_STATE  
The extension context has acquired an ActionScript BitmapData or ByteArray
object. The context cannot call this method until it releases the BitmapData or
ByteArray object.

FRE_INVALID_OBJECT  
The `arrayOrVector` or `value` FREObject parameter is invalid.

FRE_TYPE_MISMATCH  
The `arrayOrVector` FREObject parameter does not point to data that represents
an ActionScript Array or Vector class object. This return value can also mean
that the `arrayOrVector` parameter represents a Vector object and the `value`
parameter is not the correct type for that Vector object.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to set the ActionScript class object or primitive value at
the specified index of an ActionScript Array or Vector class object. The
FREObject parameter `arrayOrVector` corresponds to the Array or Vector object.
The FREObject parameter `value` corresponds to the array element value.

More Help topics

[FREGetArrayElementAt()](./fregetarrayelementat.md)

[FREGetArrayLength()](./fregetarraylength.md)
