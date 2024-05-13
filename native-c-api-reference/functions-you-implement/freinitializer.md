# FREInitializer()

#### Signature

    typedef void (*FREInitializer)(
        void**                         extDataToSet,
        FREContextInitializer*                         ctxInitializerToSet,
        FREContextFinalizer*                         contextFinalizerToSet
    );

#### Parameters

extDataToSet  
A pointer to a pointer to the extension data of the native extension. Create a
data structure to hold extension-specific data. For example, allocate the data
from the heap, or provide global data. Set extDataToSet to a pointer to the
allocated data.

ctxInitializerToSet  
A pointer to the pointer to the `FREContextInitializer()` function. Set
`ctxInitializerToSet` to the `FREContextInitializer()` function you defined.

ctxFinalizerToSet  
A pointer to the pointer to the `FREContextFinalizer()` function. Set
`ctxFinalizerToSet` to the `FREContextFinalizer()` function you defined. You can
set this pointer to `NULL`.

#### Returns

Nothing.

#### Description

The runtime calls this method once when it loads an extension. Implement this
function to do any initializations that your extension requires. Then set the
output parameters.

More Help topics

[FREContextInitializer()](./frecontextinitializer.md)

[FREContextFinalizer()](./frecontextfinalizer.md)
