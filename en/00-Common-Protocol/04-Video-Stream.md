# Video Stream

## Document Version

| Version | Date | Changes |
|---------|------|---------|
| V1.0 | 2026-06-16 | Initial version, split from original document |

## Overview

This command is used to obtain real-time video stream data from devices capable of video stream interaction (such as cameras, passport readers, iris scanners, and fingerprint readers). Upon invocation, the device will return a video stream address or continuously push image data for the upper-layer application to display or process.

## Call Flow

1. **Open Device (Open)**
   - Request: Open
   - Response: WebSocket address
   - Description: The device initializes the video stream service and returns a WebSocket address for video transmission, for example: `ws://127.0.0.1:26034/dis/hi_video`

2. **Obtain WebSocket Address**
   - The upper-layer application receives the WebSocket address returned by the device
   - Description: This address is used for establishing the video stream connection later. No video data is returned at this stage

3. **Establish WebSocket Connection**
   - The upper-layer application establishes a WebSocket connection using the obtained address
   - Connection address: `ws://127.0.0.1:26034/dis/hi_video`
   - Description: Establishes a persistent connection with the device, preparing for subsequent video data transmission

4. **Send Stream Command (TakeVideo)**
   - After the WebSocket connection is established, the upper-layer application sends the TakeVideo command
   - Description: Notifies the device to start pushing the video stream, entering a continuous video transmission state

5. **Receive Video Stream Data**
   - The device continuously pushes video frame data to the upper-layer application
   - Data format: Base64 image data
   - Description: Each frame is a Base64-encoded image, continuously pushed to form a video stream effect

6. **Video Display**
   - The upper-layer application parses and displays the received Base64 data
   - Description: Decodes Base64 into images and renders them frame by frame in real time on the interface

## TakeVideo Request Parameters

Request example:

```json
{
  "seq": "DEV_Camera_TakeVideo_${uuid}",
  "cmd": "TakeVideo",
  "datetime": "20211201130101",
  "timeout": "30000"
}
```

Parameter description:

| Parameter Name | Format | Required | Requirements |
|----------------|--------|----------|--------------|
| seq | string | Yes | DEV_Camera_TakeVideo_${uuid}, uuid serves as the unique identifier for the command |
| cmd | string | Yes | Fixed as "TakeVideo" |
| datetime | string | Yes | Command dispatch time, format: YYYYMMddHHmmss |
| timeout | string | Yes | Timeout (ms) |

## TakeVideo Response Parameters

Response example:

```json
{
  "seq": "DEV_Camera_TakeVideo_${uuid}",
  "cmd": "TakeVideo",
  "datetime": "20211201130102",
  "code": "0",
  "msg": "video stream",
  "VideoFrame": "pic_base64"
}
```

Parameter description:

| Parameter Name | Format | Required | Requirements |
|----------------|--------|----------|--------------|
| seq | string | Yes | Same as the dispatched seq |
| cmd | string | Yes | Same as the dispatched cmd |
| datetime | string | Yes | Command response time, format: YYYYMMddHHmmss |
| code | string | Yes | Refer to Common Return Codes |
| msg | string | Yes | video stream |
| VideoFrame | string | Yes | Base64 data of the image |
