# DIS 设备接口文档库

## 设备清单

| 设备类型     | 可选型号                                                     | 接口模式                                                                   |
| -------- | -------------------------------------------------------- | ---------------------------------------------------------------------- |
| 扫码枪      | [新大陆 NLS-EM28](/zh/01-扫码枪/新大陆-NLS-EM28.md)                   | Open / Scan / Stop / Close                                             |
| 扫码枪      | [牛图 NT351G](/zh/01-扫码枪/牛图-NT351G.md)                         | Open / Scan / Stop / Close                                             |
| 护照阅读器    | [ARH](/zh/02-护照阅读器/ARH.md)                                   | Open / Read / ReadChip / GetStatus / Close / Stop                      |
| 护照阅读器    | [THALES](/zh/02-护照阅读器/THALES.md)                             | Open / Read（Trace消息） / Close                                           |
| 护照阅读器    | [DESKO](/zh/02-护照阅读器/DESKO.md)                               | Open / Read / Close                                                    |
| 摄像头      | [DH DH4053S305AD](/zh/03-摄像头/DH-DH4053S305AD.md)             | 传统摄像头（Open / TakePhoto / TakeCompare / AvailNum / Close）               |
| 摄像头      | [奥尼 USB摄像头](/zh/03-摄像头/奥尼-USB摄像头.md)                         | 传统摄像头（Open / TakePhoto / TakeCompare / Close）                          |
| 摄像头      | [自助拍照服务 TRSRT](/zh/03-摄像头/TRSRT-PhotoCapturer.md)            | 自助拍照（Init / Open / Start / Stop / TakeCandidPhoto / MakePhoto / Close） |
| 凭条打印机    | [美松 MS-FPT301](/zh/04-凭条打印机/美松-MS-FPT301.md)                 | PrintImg / PrintPdf                                                    |
| 凭条打印机    | [研科 TPM80](/zh/04-凭条打印机/研科-TPM80.md)                         | Layout（图片打印 / ECL模板打印）                                                 |
| 指示灯与补光灯  | [证通](/zh/05-指示灯与补光灯/证通.md)                                   | OpLed / GetLed                                                         |
| 通断控制板    | [证通](/zh/06-通断控制板/证通.md)                                     | OnOffBoard / Reset                                                     |
| A4 打印机   | [Lexmark MS439DN](/zh/07-A4打印机/Lexmark-MS439DN.md)           | Layout / Status                                                        |
| A4 打印机   | [HP LaserJet Pro 4004](/zh/07-A4打印机/HP-LaserJet-Pro-4004.md) | Layout / Status                                                        |
| 指纹仪（四指）  | [IB Kojak](/zh/08-指纹仪/IB-Kojak-四指指纹仪.md)                     | Open / FgCollect / Stop / Close（文件路径模式）                                |
| 指纹仪（单指）  | [北京眼神](/zh/08-指纹仪/北京眼神-单指指纹仪.md)                             | Open / FgCollect / Stop / Close（文件路径模式）                                |
| 指纹仪（单指）  | [IDEMIA CB4](/zh/08-指纹仪/IDEMIA-CB4.md)                       | Open / FgCollect / FgVerify / Stop / Close（Base64模式 + Trace消息）         |
| PCSC 读卡器 | [EMP5650C](/zh/09-PCSC读卡器/EMP5650C.md)                       | Open / Read / Close                                                    |
| PCSC 读卡器 | [HID Omnikey 3121](/zh/09-PCSC读卡器/HID-Omnikey-3121.md)       | Open / ConnectCard / APDU / DisConnect / Close                         |
| 闸机底控板    | [闸机底控板](/zh/10-闸机底控板/闸机底控板.md)                               | Open（含16种cmd指令）                                                        |
| 单反       | [佳能 R100](/zh/11-单反/佳能-R100.md)                              | Open / TakePhoto / Close                                               |
| 虹膜仪      | [眼神 ECX101-80](/zh/12-虹膜仪/眼神-ECX101-80.md)                   | Open / Capture / Stop / Close                                          |
| 景深摄像头    | [Intel D415](/zh/13-景深摄像头/Intel-D415.md)                     | Open / DetectHeight / Stop / Close                                     |
| 签字屏      | [签字屏](/zh/14-签字屏/签字屏.md)                                     | Open / Write / Confirm / Clear / Stop / Close                          |
| 发证端主控    | [发证端主控](/zh/15-发证端主控/发证端主控.md)                               | Open / Action / QueryMachineActionResult / Close                       |
| 副屏控制     | [副屏控制](/zh/16-副屏控制/副屏控制.md)                                  | Open / Show / Hide / Close                                             |

## 使用方式

1. 阅读 [通用协议层](/zh/00-通用协议层/01-通讯方式与接入准备.md) 了解 DIS 服务接入方式
2. 根据项目硬件配置，从上方清单中选择对应设备文档
3. 每个设备文档自包含，可独立阅读

## 文档结构

```
DIS-API-Docs/
├── README.md
├── 00-通用协议层/
│   ├── 01-通讯方式与接入准备.md
│   ├── 03-管理接口.md
│   ├── 04-视频流获取.md
│   ├── 05-Trace消息.md
│   └── 06-通用返回码.md
├── 01-扫码枪/
│   ├── 新大陆-NLS-EM28.md
│   └── 牛图-NT351G.md
├── 02-护照阅读器/
│   ├── ARH.md
│   ├── THALES.md
│   └── DESKO.md
├── 03-摄像头/
│   ├── DH-DH4053S305AD.md
│   ├── 奥尼-USB摄像头.md
│   └── TRSRT-PhotoCapturer.md
├── 04-凭条打印机/
│   ├── 美松-MS-FPT301.md
│   └── 研科-TPM80.md
├── 05-指示灯与补光灯/
│   └── 证通.md
├── 06-通断控制板/
│   └── 证通.md
├── 07-A4打印机/
│   ├── Lexmark-MS439DN.md
│   └── HP-LaserJet-Pro-4004.md
├── 08-指纹仪/
│   ├── IB-Kojak-四指指纹仪.md
│   ├── 北京眼神-单指指纹仪.md
│   └── IDEMIA-CB4.md
├── 09-PCSC读卡器/
│   ├── EMP5650C.md
│   └── HID-Omnikey-3121.md
├── 10-闸机底控板/
│   └── 闸机底控板.md
├── 11-单反/
│   └── 佳能-R100.md
├── 12-虹膜仪/
│   └── 眼神-ECX101-80.md
├── 13-景深摄像头/
│   └── Intel-D415.md
├── 14-签字屏/
│   └── 签字屏.md
├── 15-发证端主控/
│   └── 发证端主控.md
└── 16-副屏控制/
    └── 副屏控制.md
```

<br />

## 新项目接入指南

1. 确认项目的硬件设备清单及型号
2. 从本库中挑选对应的设备文档
3. 如库中无对应型号，参照现有文档模板新建设备文档
4. 组合通用协议层 + 所需设备文档，即可形成项目接口文档

## 文档版本管理

每个设备文档独立维护版本号，修改时更新文档头部的版本记录表：

| 版本   | 日期         | 修改内容        |
| ---- | ---------- | ----------- |
| V1.0 | YYYY-MM-DD | 初始版本 / 修改说明 |

