# Management API

## Document Version

| Version | Date | Changes |
|---------|------|---------|
| V1.0 | 2026-06-16 | Initial version, split from original document |

## Query Peripheral Initialization State (CheckInitState)

Upper-layer applications can query the initialization state of peripherals through this command.

### Request Parameters

Request example:

```json
{
  "seq": "MAN_Device_CheckInitState_${uuid}",
  "cmd": "CheckInitState",
  "datetime": "20211201130101",
  "timeout": "30000",
  "param": {
    "dev_name": "00__Camera"
  }
}
```

Parameter description:

| Parameter Name | Format | Required | Requirements |
|----------------|--------|----------|--------------|
| seq | string | Yes | MAN_Device_CheckInitState_${uuid} |
| cmd | string | Yes | Fixed as "CheckInitState" |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| timeout | string | Yes | Timeout (ms) |
| param | object | No | Parameter object |
| ↳ dev_name | string | No | Device name to query state for. If empty, queries all peripheral initialization states; if "00__Camera", queries the initialization state of the camera at workstation 00 |

### Response Parameters

Response example:

```json
{
  "seq": "MAN_Device_CheckInitState_${uuid}",
  "cmd": "CheckInitState",
  "datetime": "20211201130101",
  "code": "0",
  "data": {
    "init-num": "3",
    "init-states": [
      {
        "name": "00__Camera",
        "version": "1.22.345",
        "state": "ok",
        "reason": "******"
      },
      {
        "name": "01__Camera",
        "version": "1.22.345",
        "state": "err",
        "reason": "******"
      }
    ]
  }
}
```

Parameter description:

| Parameter Name | Format | Required | Requirements |
|----------------|--------|----------|--------------|
| seq | string | Yes | Same as the dispatched seq |
| cmd | string | Yes | Same as the dispatched cmd |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| code | string | Yes | Refer to Common Return Codes |
| data | object | No | Returned data object |
| ↳ init-num | string | No | Number of peripheral initialization info nodes |
| ↳ init-states | Array | No | List of peripheral initialization info nodes |
| ↳↳ [0].name | string | Yes | Peripheral name, in "Workstation__Type" format |
| ↳↳ [0].version | string | Yes | Peripheral library version |
| ↳↳ [0].state | string | Yes | ok: initialization succeeded; err: initialization failed |
| ↳↳ [0].reason | string | No | Reason for initialization failure |

---

## Peripheral Health State Check (CheckHealthState)

It is recommended to call this command before each business session to check the running state of peripherals and ensure devices are in normal working condition.

### Request Parameters

Request example:

```json
{
  "seq": "MAN_Device_CheckHealthState_uuid",
  "cmd": "CheckHealthState",
  "timeout": "30000"
}
```

Parameter description:

| Parameter Name | Format | Required | Requirements |
|----------------|--------|----------|--------------|
| seq | string | Yes | MAN_Device_CheckHealthState_${uuid} |
| cmd | string | Yes | Fixed as "CheckHealthState" |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |

### Response Parameters

Response example:

```json
{
  "seq": "MAN_Device_CheckHealthState_uuid",
  "cmd": "CheckHealthState",
  "code": "0",
  "msg": "Success",
  "health-states": [
    {
      "name": "00__Camera",
      "code": "0",
      "healthy": true,
      "reason": ""
    },
    {
      "name": "00__QrScan",
      "code": "0",
      "healthy": false,
      "reason": "serial port open error"
    }
  ]
}
```

Parameter description:

| Parameter Name | Format | Required | Requirements |
|----------------|--------|----------|--------------|
| seq | string | Yes | Same as the dispatched seq |
| cmd | string | Yes | Same as the dispatched cmd |
| code | string | Yes | Refer to Common Return Codes |
| msg | string | No | Refer to Common Return Codes |
| health-states | Array | Yes | Returned health state list |
| ↳ [0].name | string | Yes | Peripheral name, in "Workstation__Type" format |
| ↳ [0].code | string | Yes | HealthCheck error code |
| ↳ [0].healthy | string | Yes | true: healthy; err: unhealthy |
| ↳ [0].reason | string | No | Reason for initialization failure |
