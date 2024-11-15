# Threads and native extensions

When coding your native implementation, consider the following:

- The runtime can concurrently call an extension context's FREFunction functions
  on different threads.

- The runtime can concurrently call different extension contexts' FREFunction
  functions on different threads.

Therefore, code your native implementations appropriately. For example, if you
use global data, protect it with some form of locks.

> **Note:** Your native implementation can choose to create separate threads. If
> it does, consider the restrictions specified in
> [FREObject validity](./the-freobject-type.md#freobject-validity).
