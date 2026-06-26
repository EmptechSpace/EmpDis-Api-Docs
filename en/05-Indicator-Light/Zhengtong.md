# Indicator Light & Fill Light - Zhengtong

## Document Version

| Version | Date | Changes |
|---------|------|---------|
| V1.0 | 2026-06-16 | Initial version, split from original document |
| V1.1 | 2026-06-17 | Optimized call flow diagram, added exception handling paths |

## Device Information

| Item | Details |
|------|---------|
| Device Type | Indicator Light & Fill Light |
| Brand | Zhengtong |
| DIS Interface Prefix | DEV_LightCtrl |

## Call Flow

```
OpLed (Operate LED)
GetLed (Get LED status)
```

## Interface List

### 1. Operate LED (OpLed)

#### Request Parameters

Request example:

```json
{
  "seq": "DEV_LightCtrl_OpLed_${uuid}",
  "cmd": "OpLed",
  "datetime": "20211201130101",
  "posidx": "00",
  "timeout": "30000",
  "async": "0",
  "param": {
    "LedNo": 1,
    "Status": 1
  }
}
```

Parameter description:

| Parameter Name | Format | Required | Description |
|----------------|--------|----------|-------------|
| seq | string | Yes | Request serial number: field format is business identifier prefix + underscore + unique ID |
| cmd | string | Yes | For this command, fixed as "OpLed" |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| posidx | string | Yes | Station number for multiple devices of the same type; "00"~"99" |
| timeout | string | Yes | Timeout duration (ms) |
| async | string | Yes | Asynchronous or not (default 0: synchronous); 0: synchronous; 1: asynchronous |
| param | object | Yes | Request parameters |
| ↳ LedNo | string | Yes | Light number |
| ↳ Status | string | Yes | 0: Off; 1: On; 2: Blinking |
| ↳ BlinkTime | string | Yes | Blink interval time, in ms |
| ↳ BlinkTimes | string | Yes | Number of blinks |
| ↳ Brightness | string | Yes | Light brightness |

#### Response Parameters

Response example:

```json
{
  "seq": "DEV_LightCtrl_OpLed_${uuid}",
  "cmd": "OpLed",
  "datetime": "20211201130101",
  "code": "0",
  "msg": "success",
  "posidx": "00",
  "async": "0"
}
```

Parameter description:

| Parameter Name | Format | Required | Description |
|----------------|--------|----------|-------------|
| seq | string | Yes | Same as the dispatched seq |
| cmd | string | Yes | Same as the dispatched cmd |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| code | string | Yes | Refer to control board error codes |
| msg | string | No | Refer to control board error codes |
| posidx | string | Yes | Station number for multiple devices of the same type; "00"~"99" |

---

### 2. Get LED Status (GetLed)

#### Request Parameters

Request example:

```json
{
  "seq": "DEV_LightCtrl_GetLed_${uuid}",
  "cmd": "GetLed",
  "datetime": "20211201130101",
  "posidx": "00",
  "timeout": "30000",
  "async": "1",
  "param": {
    "LedNo": "1"
  }
}
```

Parameter description:

| Parameter Name | Format | Required | Description |
|----------------|--------|----------|-------------|
| seq | string | Yes | Request serial number: field format is business identifier prefix + underscore + unique ID |
| cmd | string | Yes | For this command, fixed as "GetLed" |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| posidx | string | Yes | Station number for multiple devices of the same type; "00"~"99" |
| Timeout | string | Yes | Timeout duration (ms) |
| async | string | Yes | Asynchronous or not (default 0: synchronous); 0: synchronous; 1: asynchronous |
| param | object | Yes | Request parameters |
| ↳ LedNo | string | Yes | Light number |

#### Response Parameters

Response example:

```json
{
  "seq": "DEV_LightCtrl_GetLed_${uuid}",
  "cmd": "GetLed",
  "datetime": "20211201130101",
  "code": "0",
  "msg": "success",
  "posidx": "00",
  "async": "1",
  "data": {
    "LedNo": "1",
    "Brightness": "200",
    "Status": "1"
  }
}
```

Parameter description:

| Parameter Name | Format | Required | Description |
|----------------|--------|----------|-------------|
| seq | string | Yes | Same as the dispatched seq |
| cmd | string | Yes | Same as the dispatched cmd |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| code | string | Yes | Refer to control board error codes |
| msg | string | No | Refer to control board error codes |
| posidx | string | Yes | Station number for multiple devices of the same type; "00"~"99" |
| data | object | Yes | Returned data |
| ↳ Brightness | string | Yes | Brightness |
| ↳ Status | string | Yes | 0: Off; 1: On; 2: Blinking |

## Error Codes

| No. | Error Code | Meaning |
|-----|------------|---------|
| 1 | 17590001 | Device address error |
| 2 | 17590002 | Device command number error |
| 3 | 17590003 | Device command send error |
| 4 | 17590004 | Device sensor number error |
| 5 | 17590005 | Device stepper motor number error |
| 6 | 17590006 | Device DC motor number error |
| 7 | 17590007 | Startup process action failed |
| 8 | 17590008 | Dynamic library not initialized |
| 9 | 17590009 | Failed to get dynamic library version |

> For general return codes (0~1037), please refer to [General Return Codes](../00-通用协议层/06-通用返回码.md)
