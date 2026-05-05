# MES上位机与PLC接口文档目录

**项目：** WorkflowDrawFile / J90K  
**版本：** V1.0  
**日期：** 2026-05-05  

---

## 文档列表

| 文件名 | 类型 | 说明 |
|---|---|---|
| [MES_PLC_Map_V1.0.md](MES_PLC_Map_V1.0.md) | Markdown | Excel风格地址映射表（主文档） |
| [MES_PLC_Map_V1.0_MASTER_TO_PLC.csv](MES_PLC_Map_V1.0_MASTER_TO_PLC.csv) | CSV | MASTER→PLC信号表（可导入Excel） |
| [MES_PLC_Map_V1.0_PLC_TO_MASTER.csv](MES_PLC_Map_V1.0_PLC_TO_MASTER.csv) | CSV | PLC→MASTER推荐信号表（可导入Excel） |
| [MES_PLC_交互流程说明_V1.0.md](MES_PLC_交互流程说明_V1.0.md) | Markdown | 时序图、流程图、各阶段说明 |
| [MES_PLC_标准接口协议文档_V1.0.md](MES_PLC_标准接口协议文档_V1.0.md) | Markdown | 完整接口控制文档（ICD） |

---

## 文档说明

### Excel映射表（Map）

`MES_PLC_Map_V1.0.md` 包含三个Sheet的内容：
- **Sheet 1：MASTER TO PLC（DB201）** — 上位机写入PLC的所有信号
- **Sheet 2：PLC TO MASTER（DB200，推荐）** — PLC上报上位机的推荐信号（⚠️需确认）
- **Sheet 3：工位质量数据结构** — 每组20字节质量数据的内部结构

CSV文件可直接用Excel打开并编辑，字段与Markdown表格完全对应。

### 交互流程说明

`MES_PLC_交互流程说明_V1.0.md` 包含：
- 心跳监控时序图
- 初始化流程
- 产品到位握手时序
- 完成握手时序
- 多工位扩展说明
- 复位规则
- 超时处理
- 质量数据处理流程
- 完整时序图与Mermaid流程图

### 标准接口协议文档（ICD）

`MES_PLC_标准接口协议文档_V1.0.md` 是面向团队交付的完整协议文档，包含：
- 通信基础配置规范
- 所有信号详细定义与操作规则
- 握手协议规范
- 产品上线/返修/转线处理规范
- 质量数据规范
- 超时与异常处理规范
- 复位规范
- 接口实现要求
- 测试验证要点
- 信号速查表

---

## 使用说明

### 如何生成Excel文件

1. 下载 `MES_PLC_Map_V1.0_MASTER_TO_PLC.csv` 和 `MES_PLC_Map_V1.0_PLC_TO_MASTER.csv`
2. 用Excel打开（注意选择UTF-8编码）
3. 两个CSV文件对应两个Sheet，可复制到同一个工作簿
4. 按参考格式设置列宽、冻结标题行、添加颜色即可

### 文档阅读建议

| 角色 | 推荐阅读 |
|---|---|
| MES软件工程师 | 全部文档（重点：ICD + 流程说明） |
| PLC工程师 | Map + ICD（重点：DB201/DB200地址、握手时序） |
| 电气工程师 | Map（地址速查） |
| 测试工程师 | ICD（重点：测试验证要点） |
| 项目经理 | 流程说明（重点：总体交互架构） |

---

## 格式说明

> 本文档集格式参照 `D:\Project\25-中光学J90K\doc\中光学J90K_Map_V1.0.xlsx` 推断整理。
> 由于原始Excel文件为本地Windows路径且不在仓库中，以下格式约定为推断：
> - 列结构：通信区块/DB块/地址偏移/长度/数据格式/数据类型/Set By/Reset By/Bit标题/Bit位号/变量说明/备注
> - 分区：MASTER→PLC 和 PLC→MASTER 各为独立Sheet
> - 质量数据：独立Sheet定义内部结构

---

## 变更记录

| 版本 | 日期 | 变更内容 |
|---|---|---|
| V1.0 | 2026-05-05 | 初版建立，包含全套文档 |
