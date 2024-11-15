# Working with ActionScript ByteArray objects

Use the ActionScript ByteArray class to efficiently pass many bytes between the
ActionScript side and native side of your extension. In your native functions,
an input parameter, output parameter, or return value can correspond to an
ActionScript ByteArray class object.

As with other ActionScript class objects, an FREObject variable is the native
side representation of an ActionScript ByteArray object. The C APIs provide
functions for manipulating a ByteArray class object using an FREObject variable.
Use `FRESetObjectProperty()`, `FREGetObjectProperty()`, and
`FRECallObjectMethod()` to get and set the ActionScript ByteArray object's
properties and to call its methods.

However, to manipulate the bytes of the ByteArray object in the native code, use
the C API function
[FREAcquireByteArray()](../../native-c-api-reference/functions-you-use/freacquirebytearray.md).
This method accesses the bytes of a ByteArray object that was created on the
ActionScript side:

    FREResult FREAcquireByteArray(
        FREObject     object,
        FREByteArray* byteArrayToSet
    );
    // The type FREByteArray is defined as:

    typedef struct {
        uint32_t length;
        uint8_t* bytes;
    } FREByteArray;

After you have manipulated the bytes, use the C API
[FREReleaseByteArray()](../../native-c-api-reference/functions-you-use/frereleasebytearray.md):

    FREResult FREReleaseByteArray( FREObject object );

> **Note:** Do not call any C API functions between the calls to
> `FREAcquireByteArray()` and `FREReleaseByteArray()`. This prohibition is
> because other calls could, as a side effect, execute code that invalidates the
> pointer to the byte array contents.

#### Example

This example shows the ActionScript side of the extension creating a ByteArray
object and initializing its bytes. Then it calls a native function to manipulate
the bytes.

    // ActionScript side of the extension

    var myByteArray:ByteArray = new ByteArray();
    myByteArray.writeUTFBytes("Hello, World");
    myByteArray.position = 0;
    myExtensionContext.call("MyNativeFunction", myByteArray);


    // C code
    FREObject MyNativeFunction(FREContext ctx, void* funcData, uint32_t argc, FREObject argv[]) {
        FREByteArray byteArray;
        int retVal;

        retVal = FREAcquireByteArray(argv[0], &byteArray);
        uint8_t* nativeString = (uint8_t*) "Hello from C";
        memcpy (byteArray.bytes, nativeString, 12);
        retVal = FREReleaseByteArray(argv[0]);

        return NULL;
    }
