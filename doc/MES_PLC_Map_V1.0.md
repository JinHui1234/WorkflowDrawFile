# MES上位机与PLC交互地址映射表

**文档编号：** MES-PLC-MAP-V1.0  
**版本：** V1.0  
**日期：** 2026-05-05  
**状态：** 正式发布  
**适用项目：** WorkflowDrawFile / J90K  

---

## 格式说明

> 本文档依据参考格式（中光学J90K_Map_V1.0.xlsx）推断整理，采用相同列结构：
> 通信区块 / DB块 / 地址偏移 / 长度(Byte) / 数据格式 / 数据类型 / Set By / Reset By / Bit标题 / Bit位号 / 变量说明 / 备注
>
> 完整表格数据另见配套 CSV 文件：
> - [`MES_PLC_Map_V1.0_MASTER_TO_PLC.csv`](MES_PLC_Map_V1.0_MASTER_TO_PLC.csv)
> - [`MES_PLC_Map_V1.0_PLC_TO_MASTER.csv`](MES_PLC_Map_V1.0_PLC_TO_MASTER.csv)（推荐补充）

---

## Sheet 1：MASTER TO PLC（DB201）

### 1.1 Byte 0 — 控制位字节

| 通信区块 | DB块 | 地址偏移 | 长度(Byte) | 数据格式 | 数据类型 | Set By | Reset By | Bit标题 | Bit位号 | 变量说明 | 备注 |
|---|---|:---:|:---:|---|---|---|---|---|:---:|---|---|
| MASTER TO PLC | DB201 | 0 | 1 | BYTE | BOOL | MASTER | MASTER | 心跳 | 0 | 上位机心跳信号 | 每1秒复位/翻转一次，超过10秒无变化则报警 |
| MASTER TO PLC | DB201 | 0 | 1 | BYTE | BOOL | MASTER | MASTER | 初始化完成 | 1 | MES初始化完成标志 | 每次可执行新流程时置 True |
| MASTER TO PLC | DB201 | 0 | 1 | BYTE | BOOL | MASTER | PLC | 上位机回复到位信号 | 2 | MES收到PLC产品到位信号后的应答 | MES置 True，PLC收到后执行作业判断 |
| MASTER TO PLC | DB201 | 0 | 1 | BYTE | BOOL | MASTER | PLC | 是否作业信号 | 3 | MES判定该产品是否允许作业 | True=可作业，False=不可作业 |
| MASTER TO PLC | DB201 | 0 | 1 | BYTE | BOOL | MASTER | PLC | 上位机回复完成信号 | 4 | MES收到PLC完成信号后的应答 | MES置 True，PLC收到后复位流程 |
| MASTER TO PLC | DB201 | 0 | 1 | BYTE | BOOL | — | — | 预留 | 5 | 预留位 | — |
| MASTER TO PLC | DB201 | 0 | 1 | BYTE | BOOL | — | — | 预留 | 6 | 预留位 | — |
| MASTER TO PLC | DB201 | 0 | 1 | BYTE | BOOL | — | — | 预留 | 7 | 预留位 | — |

> **PLC地址引用：** DB201.DBX0.0 ~ DB201.DBX0.7

---

### 1.2 Byte 1 — 扩展控制位字节（工位2）

| 通信区块 | DB块 | 地址偏移 | 长度(Byte) | 数据格式 | 数据类型 | Set By | Reset By | Bit标题 | Bit位号 | 变量说明 | 备注 |
|---|---|:---:|:---:|---|---|---|---|---|:---:|---|---|
| MASTER TO PLC | DB201 | 1 | 1 | BYTE | BOOL | MASTER | PLC | 上位机回复到位信号2 | 0 | 第二工位到位应答 | MES收到PLC产品到位后置 True |
| MASTER TO PLC | DB201 | 1 | 1 | BYTE | BOOL | MASTER | PLC | 是否作业信号2 | 1 | 第二工位作业许可 | True=可作业，False=不可作业 |
| MASTER TO PLC | DB201 | 1 | 1 | BYTE | BOOL | MASTER | PLC | 上位机回复完成信号2 | 2 | 第二工位完成应答 | MES收到PLC完成信号后置 True |
| MASTER TO PLC | DB201 | 1 | 1 | BYTE | BOOL | — | — | 预留 | 3 | 预留位 | — |
| MASTER TO PLC | DB201 | 1 | 1 | BYTE | BOOL | — | — | 预留 | 4 | 预留位 | — |
| MASTER TO PLC | DB201 | 1 | 1 | BYTE | BOOL | — | — | 预留 | 5 | 预留位 | — |
| MASTER TO PLC | DB201 | 1 | 1 | BYTE | BOOL | — | — | 预留 | 6 | 预留位 | — |
| MASTER TO PLC | DB201 | 1 | 1 | BYTE | BOOL | — | — | 预留 | 7 | 预留位 | — |

> **PLC地址引用：** DB201.DBX1.0 ~ DB201.DBX1.7

---

### 1.3 Byte 2 ~ 3 — 预留字节

| 通信区块 | DB块 | 地址偏移 | 长度(Byte) | 数据格式 | 数据类型 | Set By | Reset By | Bit标题 | Bit位号 | 变量说明 | 备注 |
|---|---|:---:|:---:|---|---|---|---|---|:---:|---|---|
| MASTER TO PLC | DB201 | 2 | 1 | BYTE | BOOL | — | — | 预留 | 0~7 | Byte 2 全部预留位 | — |
| MASTER TO PLC | DB201 | 3 | 1 | BYTE | BOOL | — | — | 预留 | 0~7 | Byte 3 全部预留位 | — |

---

### 1.4 Byte 4 ~ 5 — 配置字节

| 通信区块 | DB块 | 地址偏移 | 长度(Byte) | 数据格式 | 数据类型 | Set By | Reset By | 字段名 | Bit位号 | 变量说明 | 备注 |
|---|---|:---:|:---:|---|---|---|---|---|:---:|---|---|
| MASTER TO PLC | DB201 | 4 | 1 | BYTE | BYTE | MASTER | MASTER | 产品类型 - 配方 | — | 产品型号/配方编号 | PLC依据此值选择工艺参数 |
| MASTER TO PLC | DB201 | 5 | 1 | BYTE | BYTE | — | — | 预留 | — | 预留字节 | — |

> **PLC地址引用：** DB201.DBB4，DB201.DBB5

---

### 1.5 Byte 6 ~ 45 — 产品条码（SN）

| 通信区块 | DB块 | 地址偏移 | 长度(Byte) | 数据格式 | 数据类型 | Set By | Reset By | 字段名 | 变量说明 | 备注 |
|---|---|:---:|:---:|---|---|---|---|---|---|---|
| MASTER TO PLC | DB201 | 6 | 40 | BYTE | CHAR\[40\] | MASTER | PLC | SN | 产品条码字符串 | 用于产品上线（含返修、转线）；ASCII编码，不足40字节以0x00补齐 |

> **PLC地址引用：** DB201.DBB6 ~ DB201.DBB45

---

### 1.6 Byte 46 ~ 55 — 预留字（WORD）

| 通信区块 | DB块 | 地址偏移 | 长度(Byte) | 数据格式 | 数据类型 | Set By | Reset By | 字段名 | 变量说明 | 备注 |
|---|---|:---:|:---:|---|---|---|---|---|---|---|
| MASTER TO PLC | DB201 | 46 | 2 | BYTE | WORD | — | — | 预留 | 预留字 | — |
| MASTER TO PLC | DB201 | 48 | 2 | BYTE | WORD | — | — | 预留 | 预留字 | — |
| MASTER TO PLC | DB201 | 50 | 2 | BYTE | WORD | — | — | 预留 | 预留字 | — |
| MASTER TO PLC | DB201 | 52 | 2 | BYTE | WORD | — | — | 预留 | 预留字 | — |
| MASTER TO PLC | DB201 | 54 | 2 | BYTE | WORD | — | — | 预留 | 预留字 | — |

> **PLC地址引用：** DB201.DBW46, DBW48, DBW50, DBW52, DBW54

---

### 1.7 Byte 56 ~ 255+ — 工位质量数据

| 通信区块 | DB块 | 地址偏移 | 长度(Byte) | 数据格式 | 数据类型 | Set By | Reset By | 字段名 | 变量说明 | 备注 |
|---|---|:---:|:---:|---|---|---|---|---|---|---|
| MASTER TO PLC | DB201 | 56 | 20 | 质量数据结构 | BYTES | PLC | PLC | 工位质量数据1 | 工位1质量结果数据块 | 详见工位质量数据结构定义，流程结束后由PLC复位 |
| MASTER TO PLC | DB201 | 76 | 20 | 质量数据结构 | BYTES | PLC | PLC | 工位质量数据2 | 工位2质量结果数据块 | 可扩展，最大支持10组（共200字节） |
| … | … | … | 20×N | 质量数据结构 | BYTES | PLC | PLC | 工位质量数据N | 工位N质量结果数据块 | N最大为10，地址 = 56 + (N-1)×20 |

> **注意：** 工位质量数据X的起始地址公式：**Byte_Start = 56 + (X - 1) × 20**，最多支持到工位10（Byte 236）

---

## Sheet 2：PLC TO MASTER（推荐补充，非原始提供）

> ⚠️ **说明：** 以下 PLC→MASTER 地址表为**推荐方案**，不包含在原始提供的信号点中。
> 建议使用 **DB200** 作为 PLC 向 MES 上报的数据块，具体地址需与 PLC/电气工程师确认后定版。

| 通信区块 | DB块 | 地址偏移 | 长度(Byte) | 数据格式 | 数据类型 | Set By | Reset By | Bit标题 | Bit位号 | 变量说明 | 备注 |
|---|---|:---:|:---:|---|---|---|---|---|:---:|---|---|
| PLC TO MASTER | DB200 | 0 | 1 | BYTE | BOOL | PLC | PLC | 心跳 | 0 | PLC心跳信号 | 每1秒翻转一次，MES超过10秒无变化报警 |
| PLC TO MASTER | DB200 | 0 | 1 | BYTE | BOOL | PLC | MES | 产品到位信号 | 1 | 产品到站，请求MES处理 | MES收到后开始校验SN/配方 |
| PLC TO MASTER | DB200 | 0 | 1 | BYTE | BOOL | PLC | PLC/MES | 完成信号 | 2 | 工站动作/流程完成 | 等待MES应答 |
| PLC TO MASTER | DB200 | 0 | 1 | BYTE | BOOL | PLC | PLC | 设备故障信号 | 3 | 设备异常标志 | MES可报警/记录 |
| PLC TO MASTER | DB200 | 0 | 1 | BYTE | BOOL | PLC | PLC | 治具到位信号 | 4 | 治具/夹具状态有效 | 可选，视现场定义 |
| PLC TO MASTER | DB200 | 0 | 1 | BYTE | BOOL | — | — | 预留 | 5 | 预留位 | — |
| PLC TO MASTER | DB200 | 0 | 1 | BYTE | BOOL | — | — | 预留 | 6 | 预留位 | — |
| PLC TO MASTER | DB200 | 0 | 1 | BYTE | BOOL | — | — | 预留 | 7 | 预留位 | — |
| PLC TO MASTER | DB200 | 1 | 1 | BYTE | BOOL | PLC | MES | 产品到位信号2 | 0 | 第二工位到站请求 | MES收到后返回到位应答2 |
| PLC TO MASTER | DB200 | 1 | 1 | BYTE | BOOL | PLC | MES | 完成信号2 | 1 | 第二工位完成 | 等待MES应答完成2 |
| PLC TO MASTER | DB200 | 1 | 1 | BYTE | BOOL | — | — | 预留 | 2~7 | 预留位 | — |
| PLC TO MASTER | DB200 | 4 | 1 | BYTE | BYTE | PLC | PLC | 当前产品类型 | — | PLC当前识别到的产品类型 | 可用于MES校验 |
| PLC TO MASTER | DB200 | 6 | 40 | BYTE | CHAR\[40\] | PLC | PLC | SN（设备读码结果） | — | 设备读码器扫描到的条码 | 提供给MES校验/过站 |
| PLC TO MASTER | DB200 | 46 | 2 | BYTE | WORD | PLC | PLC | 结果码 | — | 流程结果码 | 0=OK，非0=NG/异常，具体编码另定义 |
| PLC TO MASTER | DB200 | 48 | 2 | BYTE | WORD | PLC | PLC | 异常码 | — | 设备异常编号 | 0=正常，非0=具体异常原因 |
| PLC TO MASTER | DB200 | 50 | 2 | BYTE | WORD | — | — | 预留 | — | 预留字 | — |
| PLC TO MASTER | DB200 | 52 | 2 | BYTE | WORD | — | — | 预留 | — | 预留字 | — |
| PLC TO MASTER | DB200 | 54 | 2 | BYTE | WORD | — | — | 预留 | — | 预留字 | — |
| PLC TO MASTER | DB200 | 56 | 20 | 质量数据结构 | BYTES | PLC | PLC | 工位质量数据1 | 工艺质量结果 | MES读取后入库 |
| PLC TO MASTER | DB200 | 76 | 20 | 质量数据结构 | BYTES | PLC | PLC | 工位质量数据2 | 工艺质量结果扩展 | 最大10组 |

---

## Sheet 3：工位质量数据结构定义

> 每个工位质量数据块长度为 **20字节**，内部结构建议如下（具体字段需与工艺/软件确认）：

| 偏移（相对块首） | 长度(Byte) | 数据类型 | 字段名 | 说明 | 备注 |
|:---:|:---:|---|---|---|---|
| 0 | 2 | WORD | ResultCode | 质量结果码 | 0=OK，非0=NG |
| 2 | 4 | REAL | 工艺值1（如扭矩） | 实际检测值1 | 例如：扭矩 Nm |
| 6 | 4 | REAL | 工艺值2（如角度） | 实际检测值2 | 例如：角度 ° |
| 10 | 4 | REAL | 工艺值3（如时间） | 实际检测值3 | 例如：压入时间 s |
| 14 | 2 | WORD | ErrorCode | 错误代码 | 0=无错误 |
| 16 | 4 | BYTE×4 | 预留 | 预留字节 | — |

---

## 变更记录

| 版本 | 日期 | 修改内容 | 修改人 |
|---|---|---|---|
| V1.0 | 2026-05-05 | 初版建立，包含MASTER→PLC全部信号点定义，补充PLC→MASTER推荐方案 | — |

---

*本文档由 MES 接口协议文件自动整理生成，格式参照中光学J90K_Map_V1.0.xlsx推断。*
