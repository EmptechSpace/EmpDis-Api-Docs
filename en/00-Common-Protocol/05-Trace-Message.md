# Trace Message

## Document Version

| Version | Date | Changes |
|---------|------|---------|
| V1.0 | 2026-06-16 | Initial version, split from original document |

## Overview

Some peripheral commands produce interactive Trace messages during execution (such as camera services and fingerprint readers). Upper-layer applications do not need to send request commands; these are messages proactively returned by the peripheral currently executing a command. The returned Trace message has the same seq and cmd as the currently executing command, and the Trace message code value is fixed as "1031".

Upon receiving such messages, upper-layer applications can selectively perform specific actions based on their own needs. For example, after receiving a Trace message from a fingerprint reader reminding the user to lift their finger, the upper-layer application can autonomously play an audio prompt to remind the user.

## Call Flow

1. The upper-layer application sends a request command to the peripheral (not fixed)
2. The peripheral receives the request command and begins execution
3. During execution, multiple Trace messages are sent consecutively
4. After the peripheral finishes executing the command, it returns the operation result to the upper-layer application

## Response Parameters

Response example:

```json
{
  "seq": "DEV_FPrint_FgVerify_${uuid}",
  "cmd": "FgVerify",
  "datetime": "20211201130102",
  "code": "1031",
  "msg": "trace message",
  "data": {
    "event_type": "2",
    "tip_code": "9",
    "tips": "Please place finger"
  }
}
```

Parameter description:

| Parameter Name | Format | Required | Requirements |
|----------------|--------|----------|--------------|
| seq | string | Yes | Same as the seq of the currently executing command |
| cmd | string | Yes | Same as the cmd of the currently executing command |
| datetime | string | Yes | Command response time, format: YYYYMMddHHmmss |
| code | string | Yes | Fixed value: "1031" |
| msg | string | Yes | trace message |
| data | object | Yes | Varies by peripheral; refer to the corresponding peripheral documentation |
