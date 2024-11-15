# FREDispatchStatusEventAsync()

#### Usage

    FREResult FREDispatchStatusEventAsync(
            FREContext                 ctx,
            const uint8_t*                 code,
            const uint8_t*                 level
    );

#### Parameters

ctx  
An FREContext. This value is the FREContext variable that the extension context
received in its context initialization function.

code  
A pointer to a uint8_t. The runtime sets the `code` property of the StatusEvent
object to this value. Use UTF-8 encoding for the string and terminate it with
the null character.

level  
A pointer to a uint8_t. This parameter is a utf8-encoded, null-terminated
string. The runtime sets the `level` property of the StatusEvent object to this
value.

#### Returns

An FREResult. The possible return values include, but are not limited to, the
following:

FRE_OK  
The function succeeded.

FRE_INVALID_ARGUMENT  
The `ctx`, `code`, or `level` parameter is `NULL`. The runtime also returns this
value if `ctx` is not valid.

#### Description

Call this function to dispatch an ActionScript StatusEvent event. The target of
the event is the ActionScript ExtensionContext instance that the runtime
associated with the context specified by the `ctx` parameter.

Typically, the events this function dispatches are asynchronous. For example, an
extension method can start another thread to perform some task. When the task in
the other thread completes, that thread calls `FREDispatchStatusEventAsync()` to
inform the ActionScript ExtensionContext instance.

> **Note:** The `FREDispatchStatusEventAsync()` function is the only C API that
> you can call from any thread of your native implementation.

Unless one of its arguments is invalid, `FREDispatchStatusEventAsync()` return
`FRE_OK`. However, returning `FRE_OK` does not mean that the event was
dispatched. The runtime does not dispatch the event in the following cases:

- The runtime has already disposed of the ExtensionContext instance.

- The runtime is in the process of disposing of the ExtensionContext instance.

- The ExtensionContext instance has no references. It is eligible for the
  runtime garbage collector to dispose of it.

Set the `code` and `level` parameters to any null-terminated, UTF8-encoded
string values. These values are anything you want, but coordinate them with the
ActionScript side of the extension.

#### Example

More Help topics

[FREContext](../typedefs/frecontext.md)
