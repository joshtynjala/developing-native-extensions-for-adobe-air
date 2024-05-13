# FREGetArrayElementAt()

#### Usage

    FREResult FREGetArrayElementAt (
            FREObject             arrayOrVector,
            uint32_t             index,
            FREObject*             value
    );

#### Parameters

arrayOrVector  
An FREObject that represents an ActionScript Array or Vector class object.

index  
A uint32_t that contains the index of the Array or Vector element to get. The
first element of an Array or Vector object has index 0.

value  
A pointer to an FREObject. This method sets the FREObject variable that this
parameter points to. The method sets the FREObject variable to correspond to the
Array or Vector element at the requested index.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded. The `value` parameter is set to the requested Array or
Vector element.

FRE_ILLEGAL_STATE  
The extension context has acquired an ActionScript BitmapData or ByteArray
object. The context cannot call this method until it releases the BitmapData or
ByteArray object.

FRE_INVALID_ARGUMENT  
The `arrayOrVector` parameter corresponds to an ActionScript Vector object but
the `index` is greater than the index of the final element. Another reason for
this return value is if the `value` parameter is `NULL`.

FRE_INVALID_OBJECT  
The `arrayOrVector` FREObject parameter is invalid.

FRE_TYPE_MISMATCH  
The `arrayOrVector` FREObject parameter does not represent an ActionScript Array
or Vector class object.

FRE_WRONG_THREAD  
The method was called from a thread other than the one on which the runtime has
an outstanding call to a native extension function.

#### Description

Call this function to get the ActionScript class object or primitive value at
the specified index of the ActionScript Array or Vector class object. The
FREObject parameter `arrayOrVector` represents the Array or Vector object. The
runtime sets the FREObject variable that the `value` parameter points to. It
sets the FREObject variable to correspond to the appropriate Array or Vector
element.

If an ActionScript Array object does not have a value at the requested index,
the runtime sets the FREObject `value` parameter to invalid, but returns
`FRE_OK`.

More Help topics

[FRESetArrayElementAt()](./fresetarrayelementat.md)

[FRESetArrayLength()](./fresetarraylength.md)
