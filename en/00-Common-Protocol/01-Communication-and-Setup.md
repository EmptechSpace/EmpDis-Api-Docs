# Communication and Setup

## Document Version

| Version | Date | Changes |
|---------|------|---------|
| V1.0 | 2026-06-16 | Initial version, split from original document |

## DIS Service Introduction

Upper-layer applications for traditional self-service devices typically need to interface directly with various peripheral hardware such as cameras, fingerprint readers, and ID card readers. Faced with the reality of numerous peripheral brands and complex protocols, upper-layer applications must invest significant R&D resources to adapt to different device commands. Meanwhile, as hardware iteration accelerates, every time a new or replacement peripheral model is introduced, the application layer must redevelop the integration interface, resulting in repeated R&D investment, low interface reuse rates, and difficulty improving overall efficiency.

To address these pain points, Emperor Technology leverages years of technical expertise in the device domain to launch the DIS peripheral service. The DIS service uniformly encapsulates protocol parsing and functional commands for various peripherals, achieving standardized integration with all hardware categories at the lower level. Upper-layer applications only need to interface with the DIS service to achieve unified invocation of all peripherals, truly realizing one integration per device category.

Through this approach, the repeated R&D investment in hardware adaptation for upper-layer applications can be significantly reduced, system coupling is lowered, business development becomes more focused, iteration is more efficient, and genuine efficiency improvement and workload reduction are achieved.

## Overall Architecture

The architecture adopts a layered design: the upper-layer business system interacts with EmpDIS through a unified interface. EmpDIS, as the device interface service hub, is responsible for shielding lower-level device differences, unifying commands (such as Open/Read/TakePhoto/Print, etc.), and managing device states, exception handling, and retry mechanisms. The lower level connects to various peripherals, including cameras, passport readers, printers, barcode scanners, and control boards, thereby achieving decoupling and unified control between the upper layer and multiple devices.

## Communication Method

WebSocket communication is provided by default. In special cases, HTTP 1.x protocol interfaces can also be provided.

## Communication Address

- WebSocket: `ws://127.0.0.1:16001/dis/perso`
- HTTP: `http://127.0.0.1:16001/dis/perso`

When using WebSocket communication, a communication connection with EmpDIS must be established before calling management or peripheral interfaces.

## Communication Configuration

WebSocket parameter configuration details:

| Parameter | Description |
|-----------|-------------|
| Communication timeout | Can be set as needed with no mandatory requirement. When using WebSocket communication, the timeout is typically defaulted to 30000~50000ms |

## Message Format

| Item | Description |
|------|-------------|
| Server | Peripheral interface service EmpDIS |
| Client | Upper-layer APP program |
| Message format | Data is formatted as JSON messages |
| Connection type | TCP persistent connection (WebSocket) |
| Interaction mode | 1-request-1-response (WebSocket, HTTP); also supports 1-request-multiple-responses (WebSocket) |
| Verification method | MD5 |
| Maximum length | Tentatively 1MB per packet maximum |
| System requirements | Windows 7 Professional and above |
| Hardware requirements | CPU: [x86_32, x86_64, AMD64, ARM]; RAM: [8GB+]; HDD: [500GB+] |
