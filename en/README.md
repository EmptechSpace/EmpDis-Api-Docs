# EmpDIS Device API Documentation

## Device List

| Device Type | Model | Interface Mode |
|---|---|---|
| Barcode Scanner | [NLS-EM28](01-Barcode-Scanner/NLS-EM28.md) | Open / Scan / Stop / Close |
| Barcode Scanner | [NT351G](01-Barcode-Scanner/NT351G.md) | Open / Scan / Stop / Close |
| Passport Reader | [ARH](02-Passport-Reader/ARH.md) | Open / Read / ReadChip / GetStatus / Close / Stop |
| Passport Reader | [THALES](02-Passport-Reader/THALES.md) | Open / Read (Trace Message) / Close |
| Passport Reader | [DESKO](02-Passport-Reader/DESKO.md) | Open / Read / Close |
| Camera | [DH DH4053S305AD](03-Camera/DH-DH4053S305AD.md) | Traditional Camera (Open / TakePhoto / TakeCompare / AvailNum / Close) |
| Camera | [Aoni USB Camera](03-Camera/Aoni-USB-Camera.md) | Traditional Camera (Open / TakePhoto / TakeCompare / Close) |
| Camera | [TRSRT PhotoCapturer](03-Camera/TRSRT-PhotoCapturer.md) | Self-service Photo (Init / Open / Start / Stop / TakeCandidPhoto / MakePhoto / Close) |
| Receipt Printer | [MS-FPT301](04-Receipt-Printer/MS-FPT301.md) | PrintImg / PrintPdf |
| Receipt Printer | [TPM80](04-Receipt-Printer/TPM80.md) | Layout (Image Print / ECL Template Print) |
| Indicator & Fill Light | [Zhengtong](05-Indicator-Light/Zhengtong.md) | OpLed / GetLed |
| Power Control Board | [Zhengtong](06-Power-Control-Board/Zhengtong.md) | OnOffBoard / Reset |
| A4 Printer | [Lexmark MS439DN](07-A4-Printer/Lexmark-MS439DN.md) | Layout / Status |
| A4 Printer | [HP LaserJet Pro 4004](07-A4-Printer/HP-LaserJet-Pro-4004.md) | Layout / Status |
| Fingerprint Scanner (4-finger) | [IB Kojak](08-Fingerprint-Scanner/IB-Kojak.md) | Open / FgCollect / Stop / Close (File Path Mode) |
| Fingerprint Scanner (Single) | [Beijing EyeSol](08-Fingerprint-Scanner/Beijing-EyeSol-Single.md) | Open / FgCollect / Stop / Close (File Path Mode) |
| Fingerprint Scanner (Single) | [IDEMIA CB4](08-Fingerprint-Scanner/IDEMIA-CB4.md) | Open / FgCollect / FgVerify / Stop / Close (Base64 Mode + Trace Message) |
| PCSC Reader | [EMP5650C](09-PCSC-Reader/EMP5650C.md) | Open / Read / Close |
| PCSC Reader | [HID Omnikey 3121](09-PCSC-Reader/HID-Omnikey-3121.md) | Open / ConnectCard / APDU / DisConnect / Close |
| Gate Control Board | [Gate Control Board](10-Gate-Control-Board/Gate-Control-Board.md) | Open (16 cmd instructions) |
| DSLR Camera | [Canon R100](11-DSLR-Camera/Canon-R100.md) | Open / TakePhoto / Close |
| Iris Scanner | [EyeSol ECX101-80](12-Iris-Scanner/EyeSol-ECX101-80.md) | Open / Capture / Stop / Close |
| Depth Camera | [Intel D415](13-Depth-Camera/Intel-D415.md) | Open / DetectHeight / Stop / Close |
| Signature Pad | [Signature Pad](14-Signature-Pad/Signature-Pad.md) | Open / Write / Confirm / Clear / Stop / Close |
| Credential Dispenser | [Credential Dispenser](15-Credential-Dispenser/Credential-Dispenser.md) | Open / Action / QueryMachineActionResult / Close |
| Secondary Display | [Secondary Display](16-Secondary-Display/Secondary-Display.md) | Open / Show / Hide / Close |

## Getting Started

1. Read [Communication & Setup](00-Common-Protocol/01-Communication-and-Setup.md) to understand the DIS service access method
2. Select the corresponding device documentation from the list above based on your project hardware configuration
3. Each device document is self-contained and can be read independently

## Document Structure

```
EmpDis-Api-Docs/
├── index.html
├── zh/                          ← Chinese version
│   ├── README.md
│   ├── _sidebar.md
│   ├── 00-通用协议层/
│   └── ...
├── en/                          ← English version
│   ├── README.md
│   ├── _sidebar.md
│   ├── 00-Common-Protocol/
│   └── ...
├── .nojekyll
└── .gitignore
```

## New Project Integration Guide

1. Confirm the hardware device list and models for the project
2. Select the corresponding device documentation from this repository
3. If the repository does not contain the required model, create a new device document following the existing template
4. Combine the Common Protocol + required device documentation to form the project interface documentation

## Document Versioning

Each device document maintains its own version number. Update the version record table at the top of the document when making changes:

| Version | Date | Changes |
|---|---|---|
| V1.0 | YYYY-MM-DD | Initial version / Change description |
