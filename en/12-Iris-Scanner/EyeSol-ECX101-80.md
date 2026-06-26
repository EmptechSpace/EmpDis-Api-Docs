# Iris Scanner - EyeSol ECX101-80

## Document Version

| Version | Date | Changes |
|------|------|----------|
| V1.0 | 2026-06-16 | Initial version, split from original document |
| V1.1 | 2026-06-17 | Optimized call flow diagram, added exception handling paths |

## Device Information

| Item | Content |
|------|------|
| Device Type | Iris Scanner |
| Brand | EyeSol |
| Model | ECX101-80 |
| DIS Interface Prefix | DEV_Iriscope |

## Call Flow

```
Open → Capture → (Get Iris Collection Result) → Stop → Close
```

> Open returns video_url, which can be used to obtain the iris scanner preview video stream. For the process, please refer to General Protocol Layer - Video Stream Acquisition.

## Interface List

### 1. Open Iris Scanner (Open)

Through this command, the upper-layer application can open the iris scanner. For the video stream acquisition process, please refer to General Protocol Layer - Video Stream Acquisition.

#### Request Parameters

Request Example:

```json
{
  "seq": "DEV_Iriscope_Open_${uuid}",
  "cmd": "Open",
  "datetime": "20211201130101",
  "posidx": "00",
  "timeout": "30000",
  "async": "0"
}
```

Parameter Description:

| Parameter Name | Format | Required | Description |
|----------|------|----------|----------|
| seq | string | Yes | DEV_Iriscope_Open_${uuid} |
| cmd | string | Yes | Fixed as "Open" |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| posidx | string | Yes | Station number for multiple devices of the same type; "00"~"99" |
| timeout | string | Yes | Timeout (ms) |
| async | string | Yes | Async flag (default 0: synchronous); 0: synchronous; 1: asynchronous |

#### Return Parameters

Return Example:

```json
{
  "seq": "DEV_Iriscope_Open_${uuid}",
  "cmd": "Open",
  "datetime": "20211201130102",
  "code": "0",
  "msg": "Success",
  "suggest": "",
  "posidx": "00",
  "DllVersion": "V6.24.703.1",
  "data": {
    "video_url": [
      {
        "00": "ws://127.0.0.1:62383/dis/hi_video"
      }
    ]
  }
}
```

Parameter Description:

| Parameter Name | Format | Required | Description |
|----------|------|----------|----------|
| seq | string | Yes | Same as the dispatched seq |
| cmd | string | Yes | Same as the dispatched cmd |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| code | string | Yes | Refer to General Return Codes / Iris Scanner Return Codes |
| msg | string | No | Prompt message |
| suggest | string | No | Suggestion |
| posidx | string | Yes | Station number for multiple devices of the same type; "00"~"99" |
| DllVersion | string | No | Peripheral library version number |
| data | object | No | Return data |
| ↳ video_url | array | Yes | Iris scanner preview video stream address |

---

### 2. Iris Capture (Capture)

Through this command, the upper-layer application can start collecting iris data using the iris scanner.

#### Request Parameters

Request Example:

```json
{
  "seq": "DEV_Iriscope_Capture_${uuid}",
  "cmd": "Capture",
  "datetime": "20211201130101",
  "param": {
    "PersoIris": "D:/Iriscope/",
    "EyeFlag": "3",
    "Compress": "80"
  },
  "posidx": "00",
  "async": "0"
}
```

Parameter Description:

| Parameter Name | Format | Required | Description |
|----------|------|----------|----------|
| seq | string | Yes | DEV_Iriscope_Capture_${uuid} |
| cmd | string | Yes | Fixed as "Capture" |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| posidx | string | Yes | Station number for multiple devices of the same type; "00"~"99" |
| timeout | string | Yes | Timeout (ms) |
| async | string | Yes | Async flag (default 0: synchronous); 0: synchronous; 1: asynchronous |
| param | object | Yes | Parameter object |
| ↳ PersoIris | string | Yes | Iris data save path |
| ↳ EyeFlag | string | Yes | Eye flag; "1": left eye; "2": right eye; "3": both eyes |
| ↳ Compress | string | No | Compression quality; default "80" |

#### Return Parameters

Return Example:

```json
{
  "seq": "DEV_Iriscope_Capture_${uuid}",
  "cmd": "Capture",
  "datetime": "20211201130102",
  "code": "0",
  "msg": "Success",
  "suggest": "",
  "data": {
    "Iris_model": "3",
    "PersoIris": "D:/Iriscope/Iris.jpg",
    "Iris_Feature": "D:/Iriscope/Iris_Feature.txt",
    "Iris_Crop_Right": "D:/Iriscope/Iris_Crop_Right.jpg",
    "Iris_Feature_Right": "D:/Iriscope/Iris_Feature_Right.txt",
    "Iris_Score_Right": "80",
    "Iris_Crop_Left": "D:/Iriscope/Iris_Crop_Left.jpg",
    "Iris_Feature_Left": "D:/Iriscope/Iris_Feature_Left.txt",
    "Iris_Score_Left": "80"
  }
}
```

Parameter Description:

| Parameter Name | Format | Required | Description |
|----------|------|----------|----------|
| seq | string | Yes | Same as the dispatched seq |
| cmd | string | Yes | Same as the dispatched cmd |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| code | string | Yes | Refer to General Return Codes / Iris Scanner Return Codes |
| msg | string | No | Prompt message |
| suggest | string | No | Suggestion |
| data | object | No | Return data |
| ↳ Iris_model | string | Yes | Iris mode; "3": both eyes |
| ↳ PersoIris | string | Yes | Iris image save path |
| ↳ Iris_Feature | string | Yes | Iris feature value file path |
| ↳ Iris_Crop_Right | string | No | Right eye cropped image path |
| ↳ Iris_Feature_Right | string | No | Right eye feature value file path |
| ↳ Iris_Score_Right | string | No | Right eye iris quality score |
| ↳ Iris_Crop_Left | string | No | Left eye cropped image path |
| ↳ Iris_Feature_Left | string | No | Left eye feature value file path |
| ↳ Iris_Score_Left | string | No | Left eye iris quality score |

---

### 3. Stop Capture (Stop)

When the upper-layer business needs to abort the current processing flow, this command can be called to end the ongoing operation.

#### Request Parameters

Request Example:

```json
{
  "seq": "DEV_Iriscope_Stop_${uuid}",
  "cmd": "Stop",
  "datetime": "20211201130101",
  "async": "1",
  "timeout": "30000",
  "posidx": "00"
}
```

Parameter Description:

| Parameter Name | Format | Required | Description |
|----------|------|----------|----------|
| seq | string | Yes | DEV_Iriscope_Stop_${uuid} |
| cmd | string | Yes | Fixed as "Stop" |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| posidx | string | Yes | Station number for multiple devices of the same type; "00"~"99" |
| timeout | string | Yes | Timeout (ms) |
| async | string | Yes | Async flag (recommended 1); 0: synchronous; 1: asynchronous |

#### Return Parameters

Return Example:

```json
{
  "seq": "DEV_Iriscope_Stop_${uuid}",
  "cmd": "Stop",
  "datetime": "20211201130102",
  "code": "0",
  "msg": "Success",
  "suggest": "",
  "posidx": "00",
  "DllVersion": "V6.24.703.1"
}
```

Parameter Description:

| Parameter Name | Format | Required | Description |
|----------|------|----------|----------|
| seq | string | Yes | Same as the dispatched seq |
| cmd | string | Yes | Same as the dispatched cmd |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| code | string | Yes | Refer to General Return Codes / Iris Scanner Return Codes |
| msg | string | No | Prompt message |
| suggest | string | No | Suggestion |
| posidx | string | Yes | Station number for multiple devices of the same type; "00"~"99" |
| DllVersion | string | No | Peripheral library version number |

---

### 4. Close Iris Scanner (Close)

Through this command, the upper-layer application can close the iris scanner.

#### Request Parameters

Request Example:

```json
{
  "seq": "DEV_Iriscope_Close_${uuid}",
  "cmd": "Close",
  "datetime": "20211201130101",
  "timeout": "30000",
  "posidx": "00",
  "async": "0"
}
```

Parameter Description:

| Parameter Name | Format | Required | Description |
|----------|------|----------|----------|
| seq | string | Yes | DEV_Iriscope_Close_${uuid} |
| cmd | string | Yes | Fixed as "Close" |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| posidx | string | Yes | Station number for multiple devices of the same type; "00"~"99" |
| timeout | string | Yes | Timeout (ms) |
| async | string | Yes | Async flag (default 0: synchronous); 0: synchronous; 1: asynchronous |

#### Return Parameters

Return Example:

```json
{
  "seq": "DEV_Iriscope_Close_${uuid}",
  "cmd": "Close",
  "datetime": "20211201130102",
  "code": "0",
  "posidx": "00",
  "msg": "Success",
  "suggest": ""
}
```

Parameter Description:

| Parameter Name | Format | Required | Description |
|----------|------|----------|----------|
| seq | string | Yes | Same as the dispatched seq |
| cmd | string | Yes | Same as the dispatched cmd |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| code | string | Yes | Refer to General Return Codes / Iris Scanner Return Codes |
| msg | string | No | Prompt message |
| suggest | string | No | Suggestion |
| posidx | string | Yes | Station number for multiple devices of the same type; "00"~"99" |

## Error Codes

| No. | Error Code | Meaning |
|------|--------|------|
| 1 | 15700001 | Timeout |
| 2 | 15700003 | Invalid pointer |
| 3 | 15700004 | This service function is not supported |
| 4 | 15700005 | Insufficient memory |
| 5 | 15700006 | Thread resume failed |
| 6 | 15700007 | Thread creation failed |
| 7 | 15700008 | Event creation failed |
| 8 | 15700009 | Command execution failed |
| 9 | 15700010 | Command execution timeout |
| 10 | 99999999 | Unknown error |
| 11 | 15700101 | Device not opened |
| 12 | 15700107 | Device busy |
| 13 | 15700109 | Device already opened, already initialized |
| 14 | 15700110 | Device does not exist |
| 15 | 15700113 | Device communication failed |
| 16 | 15700114 | Device operation failed |
| 17 | 15700115 | Device not supported |
| 18 | 15700116 | Invalid device handle |
| 19 | 15700117 | Initialization failed |

> For general return codes (0~1037), please refer to [General Return Codes](../00-Common-Protocol/06-Common-Return-Codes.md)
