# Power Control Board - Zhengtong

## Document Version

| Version | Date | Changes |
|---------|------|---------|
| V1.0 | 2026-06-16 | Initial version, split from original document |
| V1.1 | 2026-06-17 | Optimized call flow diagram, added exception handling paths |

## Device Information

| Item | Details |
|------|---------|
| Device Type | Power Control Board |
| Brand | Zhengtong |
| DIS Interface Prefix | DEV_IOControl |

## Call Flow

When a device open failure occurs during normal hardware operation, consider resetting the device and reopening the hardware.

```
OnOffBoard (Power control board on/off)
Reset (Power control board reset)
```

## Interface List

### 1. Power Control Board On/Off (OnOffBoard)

Control the specified channel of the power control board to connect or disconnect.

#### Request Parameters

Request example:

```json
{
  "seq": "DEV_IOControl_OnOffBoard_${uuid}",
  "Timeout": "30000",
  "cmd": "OnOffBoard",
  "datetime": "20211201130101",
  "param": {
    "Channel": "4",
    "Nid": "1",
    "Status": "1"
  },
  "posidx": "00",
  "async": "0"
}
```

Parameter description:

| Parameter Name | Format | Required | Description |
|----------------|--------|----------|-------------|
| seq | string | Yes | Request serial number: field format is business identifier prefix + underscore + unique ID |
| cmd | string | Yes | For this command, fixed as "OnOffBoard" |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| posidx | string | Yes | Station number for multiple devices of the same type; "00"~"99" |
| Timeout | string | Yes | Timeout duration (ms) |
| async | string | Yes | Asynchronous or not (default 0: synchronous); 0: synchronous; 1: asynchronous |
| param | object | Yes | Request parameters |
| ↳ Nid | string | Yes | Power control board sequence number, value from 1 to 4 (supports connecting multiple control boards; generally fill in 1 when only one is connected) |
| ↳ Channel | string | Yes | USB channel number on the control board, value from 1 to 4 (corresponding to USB ports 1 to 4 on the control board) |
| ↳ Status | string | Yes | On/off operation for the Channel number: 1 connect, 2 disconnect, 3 reset |

#### Response Parameters

Response example:

```json
{
  "seq": "DEV_IOControl_OnOffBoard_${uuid}",
  "Timeout": "30000",
  "cmd": "OnOffBoard",
  "datetime": "20211201130101",
  "data": {},
  "code": "0",
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
| code | string | Yes | Refer to power control board error codes |
| msg | string | No | Refer to power control board error codes |
| posidx | string | Yes | Station number for multiple devices of the same type; "00"~"99" |

---

### 2. Power Control Board Reset (Reset)

#### Request Parameters

Request example:

```json
{
  "seq": "DEV_IOControl_Reset_${uuid}",
  "Timeout": "30000",
  "cmd": "Reset",
  "datetime": "20211201130101",
  "param": {
    "Channel": "1"
  },
  "posidx": "00",
  "async": "0"
}
```

Parameter description:

| Parameter Name | Format | Required | Description |
|----------------|--------|----------|-------------|
| seq | string | Yes | Request serial number: field format is business identifier prefix + underscore + unique ID |
| cmd | string | Yes | For this command, fixed as "Reset" |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| posidx | string | Yes | Station number for multiple devices of the same type; "00"~"99" |
| Timeout | string | Yes | Timeout duration (ms) |
| async | string | Yes | Asynchronous or not (default 0: synchronous); 0: synchronous; 1: asynchronous |
| param | object | Yes | Request parameters |
| ↳ Channel | string | Yes | Power control board sequence number, value from 1 to 4 (supports connecting multiple control boards; generally fill in 1 when only one is connected) |

#### Response Parameters

Response example:

```json
{
  "seq": "DEV_IOControl_Reset_${uuid}",
  "Timeout": "30000",
  "cmd": "Reset",
  "datetime": "20211201130101",
  "data": {},
  "code": "0",
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
| code | string | Yes | Refer to power control board error codes |
| msg | string | No | Refer to power control board error codes |
| posidx | string | Yes | Station number for multiple devices of the same type; "00"~"99" |

## Error Codes

| No. | Error Code | Meaning |
|-----|------------|---------|
| 1 | 17690001 | Initialization failed |
| 2 | 17690002 | On/off operation failed |
| 3 | 17690003 | Reset failed |
| 4 | 17690004 | Failed to get library version |
| 5 | 17696001 | Command not supported |

> For general return codes (0~1037), please refer to [General Return Codes](../00-通用协议层/06-通用返回码.md)
