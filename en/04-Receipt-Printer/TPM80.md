# Receipt Printer - TPM80

## Document Version

| Version | Date | Changes |
|---------|------|---------|
| V1.0 | 2026-06-16 | Initial version, split from original document |
| V1.1 | 2026-06-17 | Optimized call flow diagram, added exception handling paths |

## Device Information

| Item | Details |
|------|---------|
| Device Type | Receipt Printer |
| Brand | Yanke |
| Model | TPM80 |
| DIS Interface Prefix | DEV_SlipPrinter |

## Call Flow

```mermaid
flowchart TD
    START([Start]) --> CHOOSE{Select print method}
    CHOOSE -->|Image printing| IMG[Layout - Image printing]
    CHOOSE -->|ECL template printing| ECL[Layout - ECL template printing]
    IMG -->|code=0 Print successful| OK[Print completed]
    IMG -->|14203004 Image loading failed| ERR1[Check image path]
    IMG -->|14299603 Out of paper| ERR2[Printer out of paper]
    ECL -->|code=0 Print successful| OK
    ECL -->|14203003 ECL template to image conversion failed| ERR3[Check template file]
    ECL -->|14299603 Out of paper| ERR2
    ERR1 --> RETRY{Retry?}
    ERR2 --> FIX[Add paper and retry]
    ERR3 --> RETRY
    RETRY -->|Yes| CHOOSE
    RETRY -->|No| END2([End])
    FIX --> CHOOSE
    OK --> END([End])

    classDef success fill:#d4edda,stroke:#28a745,color:#155724
    classDef error fill:#f8d7da,stroke:#dc3545,color:#721c24
    classDef action fill:#cce5ff,stroke:#007bff,color:#004085
    classDef warning fill:#fff3cd,stroke:#ffc107,color:#856404
    class START,END,END2,OK success
    class ERR1,ERR2,ERR3 error
    class IMG,ECL,FIX action
    class CHOOSE,RETRY warning
```

> The print module uses direct invocation and does not involve device open and close operations.

## Interface List

### 1. Image Printing (Layout)

Through this command, the upper-layer application can use the receipt printer for image printing.

#### Request Parameters

Request example:

```json
{
  "seq": "DEV_SlipPrinter_Layout_${uuid}",
  "cmd": "Layout",
  "datetime": "20211201130101",
  "timeout": "30000",
  "posidx": "00",
  "async": "0",
  "param": {
    "PicPath": "/home/judy/test.bmp",
    "PicType": "bmp"
  }
}
```

Parameter description:

| Parameter Name | Format | Required | Description |
|----------------|--------|----------|-------------|
| seq | string | Yes | DEV_SlipPrinter_Layout_${uuid} |
| cmd | string | Yes | Fixed as "Layout" |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| posidx | string | Yes | Station number for multiple devices of the same type; "00"~"99" |
| timeout | string | Yes | Timeout duration (ms) |
| async | string | Yes | Asynchronous or not (default 0: synchronous); 0: synchronous; 1: asynchronous |
| param | object | Yes | Parameter object |
| ↳ PicPath | string | Yes | Image path |
| ↳ PicType | string | Yes | Image type (e.g. bmp) |

#### Response Parameters

Response example:

```json
{
  "seq": "DEV_SlipPrinter_Layout_${uuid}",
  "cmd": "Layout",
  "datetime": "20211201130102",
  "code": "0",
  "msg": "Success",
  "posidx": "00"
}
```

Parameter description:

| Parameter Name | Format | Required | Description |
|----------------|--------|----------|-------------|
| seq | string | Yes | Same as the dispatched seq |
| cmd | string | Yes | Same as the dispatched cmd |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| code | string | Yes | Refer to general return codes / receipt printer error codes |
| msg | string | No | Refer to general return codes / receipt printer error codes |
| posidx | string | Yes | Same as the requested posidx |

---

### 2. ECL Template Printing (Layout)

This interface is used to call the receipt printer to execute printing operations. In ECL printing mode, the system pre-defines the print format and dynamic fields based on the template provided by the customer. When the upper-layer application calls it, only the dynamic field data (such as name, business number, generation time, etc.) needs to be passed in, and the system will automatically render the template and output the printed content.

#### Request Parameters

Request example:

```json
{
  "seq": "DEV_SlipPrinter_Layout_${uuid}",
  "cmd": "Layout",
  "datetime": "20211201130101",
  "timeout": "30000",
  "posidx": "00",
  "async": "0",
  "param": {
    "CfgName": "D:/test.ecl",
    "Name": "Test",
    "Sex": "M",
    "Number": "123456789"
  }
}
```

Parameter description:

| Parameter Name | Format | Required | Description |
|----------------|--------|----------|-------------|
| seq | string | Yes | DEV_SlipPrinter_Layout_${uuid} |
| cmd | string | Yes | Fixed as "Layout" |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| posidx | string | Yes | Station number for multiple devices of the same type; "00"~"99" |
| timeout | string | Yes | Timeout duration (ms) |
| async | string | Yes | Asynchronous or not (default 0: synchronous); 0: synchronous; 1: asynchronous |
| param | object | Yes | Parameter object |
| ↳ CfgName | string | Yes | ECL template file path |
| ↳ Other fields | string | No | Dynamic fields defined in the template; field names must match the variable names defined in the template |

#### Response Parameters

Response example:

```json
{
  "seq": "DEV_SlipPrinter_Layout_${uuid}",
  "cmd": "Layout",
  "datetime": "20211201130102",
  "code": "0",
  "msg": "Success",
  "suggest": "",
  "posidx": "00"
}
```

Parameter description:

| Parameter Name | Format | Required | Description |
|----------------|--------|----------|-------------|
| seq | string | Yes | Same as the dispatched seq |
| cmd | string | Yes | Same as the dispatched cmd |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| code | string | Yes | Refer to general return codes / receipt printer error codes |
| msg | string | No | Refer to general return codes / receipt printer error codes |
| suggest | string | No | Suggestion |
| posidx | string | Yes | Same as the requested posidx |

## Error Codes

| No. | Error Code | Meaning |
|-----|------------|---------|
| 1 | 99999901 | Active cancel |
| 2 | 14203001 | Device not opened |
| 3 | 14203002 | Dispatched parameter error |
| 4 | 14203003 | ECL template to image conversion failed |
| 5 | 14203004 | Image loading failed |
| 6 | 14203005 | Unsupported command |
| 7 | 14203006 | Failed to get printer status |
| 8 | 14203007 | SDK returned failure |
| 9 | 14203008 | SDK loading failed |
| 10 | 14203009 | Printer status abnormal |
| 11 | 14299601 | Printer offline |
| 12 | 14299602 | Printer paper jam |
| 13 | 14299603 | Printer out of paper |
| 14 | 14299604 | Paper running low |
| 15 | 14299605 | Unknown error |
| 16 | 14299606 | Printer cover open |
| 17 | 14299607 | Printer overheated |
| 18 | 14299608 | Cutter error |

> For general return codes (0~1037), please refer to [General Return Codes](../00-Common-Protocol/06-Common-Return-Codes.md)
