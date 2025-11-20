# Base
### ST_MethodState [Struct]
> **ST\_MethodState** is a standardized structure for tracking the lifecycle of a method or request.
> It indicates when a method has just **started** (`Init`), is **actively executing** (`Execute`), or has **failed to complete within the allowed time** (`Timeout`, default 5s).

| Variable   | Type  | Description |
|------------|-------|-------------|
| **init**    | BOOL  | TRUE only during the **first execution cycle** of a method. Resets automatically in the next cycle. |
| **execute** | BOOL  | TRUE while the method is **actively processing** the request. |
| **timeout** | BOOL  | TRUE if the method **did not complete** within the specified timeout (default = 5 s). |
---

### FB_DeviceBase [Function block]
> FB_DeviceBase is the core function block of the TcNexa framework, designed to be extended by every device in the system.
> It provides shared logic, standardized methods, and common properties, ensuring consistent behavior across all devices.
> By inheriting from FB_DeviceBase, new devices gain built-in features such as initialization handling, execution cycles, error management, and diagnostics, reducing code duplication and simplifying integration.

**FB_init** [Method]
> FB_Init is a standardized initialization function block used in TcNexa devices.
> It extends the default TwinCAT initialization logic with additional fields: Name, Id, and Timeout.
> These extra variables allow each device to be uniquely identified, labeled for diagnostics, and initialized with a controlled maximum method time.

This function block is typically called once during the first PLC cycle to prepare a device for operation.

_Inputs_
| Variable    | Type      | Description |
|-------------|-----------|-------------|
| **Name**    | STRING | A human-readable name for the device, used for diagnostics and logging. |
| **Id**      | STRING | Unique numeric identifier for the device instance. |
| **Timeout** | TIME   | Maximum allowed time for the method call. If exceeded, the method fails and an error is triggered. |

**FB_main** [Mehtod]
> FB_Main is the core cyclic function block for each TcNexa device.
> It is intended to be called at each PLC cycle and executes the device’s background logic, including state machine updates, method execution, error handling, diagnostics, and other tasks.


---
