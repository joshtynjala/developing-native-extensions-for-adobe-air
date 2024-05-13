# Threads and native extensions

When coding your Java implementation, consider the following:

- The runtime can concurrently call an extension context's FREFunction functions
  on different threads.

- The runtime can concurrently call different extension contexts' FREFunction
  functions on different threads.

Therefore, code your Java implementations appropriately. For example, if you use
global data, protect it with some form of locks.

> Note: Your Java implementation can choose to create separate threads. If it
> does, consider the restrictions specified in
> [FREObject validity](./accessing-actionscript-objects.md#freobject-validity).
