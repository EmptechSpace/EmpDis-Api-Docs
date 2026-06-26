# A4 打印机 - Lexmark MS439DN

## 文档版本

| 版本 | 日期 | 修改内容 |
|------|------|----------|
| V1.0 | 2026-06-16 | 初始版本，从原始文档拆分 |

## 设备信息

| 项目 | 内容 |
|------|------|
| 设备类型 | A4 打印机 |
| 品牌 | Lexmark |
| 型号 | MS439DN |
| DIS 接口前缀 | DEV_Printer |

## 调用流程

```mermaid
flowchart TD
    START([开始]) --> CHOOSE{选择操作}
    CHOOSE -->|打印| LAYOUT[Layout 打印]
    CHOOSE -->|查询状态| STATUS[Status 获取打印状态]
    LAYOUT -->|code=0 打印成功| OK1[打印完成]
    LAYOUT -.->|code≠0 打印失败| ERR1[处理打印异常]
    STATUS -->|code=0 状态正常| OK2[打印机状态正常]
    STATUS -.->|状态异常| ERR2[打印机缺纸/卡纸/脱机]
    OK1 --> END1([结束])
    OK2 --> END2([结束])
    ERR1 --> RETRY{是否重试?}
    RETRY -->|是| CHOOSE
    RETRY -->|否| END3([结束])
    ERR2 --> FIX[人工干预后重试]
    FIX --> CHOOSE

    classDef success fill:#d4edda,stroke:#28a745,color:#155724
    classDef error fill:#f8d7da,stroke:#dc3545,color:#721c24
    classDef action fill:#cce5ff,stroke:#007bff,color:#004085
    classDef warning fill:#fff3cd,stroke:#ffc107,color:#856404
    class START,END1,END2,END3,OK1,OK2 success
    class ERR1,ERR2 error
    class LAYOUT,STATUS,FIX action
    class CHOOSE,RETRY warning
```

> 注意：A4 打印机接口在部分版本中已移除，请根据实际项目配置确认是否可用。

## 接口列表

### 1. 打印（Layout）

#### 请求参数

请求示例：

```json
{
  "seq": "DEV_Printer_Layout_${uuid}",
  "cmd": "Layout",
  "datetime": "20211201130101",
  "posidx": "00",
  "timeout": "30000",
  "async": "0",
  "param": {
    "source": "",
    "PrintName": "",
    "Url1": "",
    "Url2": "",
    "DocType": "",
    "Copy": "1",
    "Orientation": "",
    "PageSize": "",
    "PageMargins": "",
    "Sided": ""
  }
}
```

参数说明：

| 参数名称 | 格式 | 是否必填 | 参数说明 |
|----------|------|----------|----------|
| seq | string | 是 | 请求序列号：字段格式为业务标识头+下划线+唯一号 |
| cmd | string | 是 | 本指令下，固定为"Layout" |
| datetime | string | 是 | 指令的下发时间，格式：YYYYMMddHHmmss |
| posidx | string | 是 | 多个同款设备的工位号；"00"~"99" |
| timeout | string | 是 | 超时时间(ms) |
| async | string | 是 | 是否异步（默认0:同步）；0：同步；1：异步 |
| param | object | 是 | 参数对象 |
| ↳ source | string | 是 | 打印内容来源 |
| ↳ PrintName | string | 否 | 打印机名称 |
| ↳ Url1 | string | 否 | 打印地址1 |
| ↳ Url2 | string | 否 | 打印地址2 |
| ↳ DocType | string | 否 | 文档类型 |
| ↳ Copy | string | 否 | 打印份数 |
| ↳ Orientation | string | 否 | 打印方向 |
| ↳ PageSize | string | 否 | 纸张大小 |
| ↳ PageMargins | string | 否 | 页边距 |
| ↳ Sided | string | 否 | 单双面打印 |

#### 返回参数

返回示例：

```json
{
  "seq": "DEV_Printer_Layout_${uuid}",
  "cmd": "Layout",
  "datetime": "20211201130102",
  "code": "0",
  "msg": "success",
  "posidx": "00"
}
```

参数说明：

| 参数名称 | 格式 | 是否必填 | 参数说明 |
|----------|------|----------|----------|
| seq | string | 是 | 同下发的 seq |
| cmd | string | 是 | 同下发的 cmd |
| datetime | string | 是 | 指令的下发时间，格式：YYYYMMddHHmmss |
| code | string | 是 | 参照通用返回码 / A4 打印机错误码 |
| msg | string | 否 | 参照通用返回码 / A4 打印机错误码 |
| posidx | string | 是 | 多个同款设备的工位号；"00"~"99" |

---

### 2. 获取打印状态（Status）

#### 请求参数

请求示例：

```json
{
  "seq": "DEV_Printer_Status_${uuid}",
  "cmd": "Status",
  "datetime": "20211201130101",
  "posidx": "00",
  "timeout": "30000",
  "async": "0"
}
```

参数说明：

| 参数名称 | 格式 | 是否必填 | 参数说明 |
|----------|------|----------|----------|
| seq | string | 是 | 请求序列号：字段格式为业务标识头+下划线+唯一号 |
| cmd | string | 是 | 本指令下，固定为"Status" |
| datetime | string | 是 | 指令的下发时间，格式：YYYYMMddHHmmss |
| posidx | string | 是 | 多个同款设备的工位号；"00"~"99" |
| timeout | string | 是 | 超时时间(ms) |
| async | string | 是 | 是否异步（默认0:同步）；0：同步；1：异步 |

#### 返回参数

返回示例：

```json
{
  "seq": "DEV_Printer_Status_${uuid}",
  "cmd": "Status",
  "datetime": "20211201130102",
  "code": "0",
  "msg": "success",
  "posidx": "00",
  "data": {
    "PrinterStatus": "",
    "TonerStatus": "",
    "PaperStatus": "",
    "Toner": "",
    "Life": "",
    "Black": "",
    "Color": ""
  }
}
```

参数说明：

| 参数名称 | 格式 | 是否必填 | 参数说明 |
|----------|------|----------|----------|
| seq | string | 是 | 同下发的 seq |
| cmd | string | 是 | 同下发的 cmd |
| datetime | string | 是 | 指令的下发时间，格式：YYYYMMddHHmmss |
| code | string | 是 | 参照通用返回码 / A4 打印机错误码 |
| msg | string | 否 | 参照通用返回码 / A4 打印机错误码 |
| posidx | string | 是 | 多个同款设备的工位号；"00"~"99" |
| data | object | 否 | 返回数据 |
| ↳ PrinterStatus | string | 否 | 打印机状态 |
| ↳ TonerStatus | string | 否 | 碳粉状态 |
| ↳ PaperStatus | string | 否 | 纸张状态 |
| ↳ Toner | string | 否 | 碳粉余量 |
| ↳ Life | string | 否 | 寿命 |
| ↳ Black | string | 否 | 黑色碳粉 |
| ↳ Color | string | 否 | 彩色碳粉 |

## 错误码

| 序号 | 错误码 | 含义 |
|------|--------|------|
| 1 | 14731002 | 设备自身故障 |
| 2 | 14731203 | 打开文件标识符失败 |
| 3 | 14734001 | 缺少必备参数 |
| 4 | 14734002 | 字段或者参数非法 |
| 5 | 14734004 | JSON 格式非法 |
| 6 | 14734202 | 文件无法访问 |
| 7 | 14739003 | 当前任务失败 |
| 8 | 14739006 | 加载图片失败 |
| 9 | 14739007 | 打印图片失败 |

> 通用返回码（0~1037）请参阅 [通用返回码](../00-通用协议层/06-通用返回码.md)
