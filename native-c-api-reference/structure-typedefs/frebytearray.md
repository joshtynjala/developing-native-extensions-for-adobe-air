# FREByteArray

Use the FREByteArray structure when acquiring and manipulating the bytes in an
ActionScript ByteArray class object. The structure is defined as follows:

    typedef struct {
        uint32_t            length;
        uint8_t*            bytes;
    } FREByteArray;

The fields of FREByteArray have the following meanings:

length  
A uint32_t that is the number of bytes in the `bytes` array.

bytes  
A uint8_t\* that is a pointer to the bytes in the ActionScript ByteArray object.

More Help topics

[FREAcquireByteArray()](../functions-you-use/freacquirebytearray.md)
