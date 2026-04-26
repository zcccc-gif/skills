---
name: xlsx-zh
description: "当用户需要处理电子表格文件（.xlsx、.xlsm、.csv、.tsv）时使用此技能。触发条件包括：打开、读取、编辑或修复现有电子表格（如添加列、计算公式、格式化、制图、清理杂乱数据）；从零创建新电子表格；在不同表格格式之间转换。当用户提及电子表格文件名或路径时尤其适用。也适用于清理或重组格式混乱的数据文件。交付物必须是电子表格文件。"
---

# XLSX 电子表格创建、编辑与分析

## 输出要求

### 专业字体
- 使用统一的专业字体（如微软雅黑、宋体、Arial）

### 零公式错误
- 每个 Excel 模型必须零公式错误（#REF!、#DIV/0!、#VALUE!、#N/A、#NAME?）

### 保留现有模板
- 修改文件时精确匹配现有格式、样式和约定
- 现有模板规范始终优先于这些指南

## 财务模型

### 颜色编码标准

#### 行业标准颜色约定
- **蓝色文字（RGB: 0,0,255）**：硬编码输入，用户可修改的数字
- **黑色文字（RGB: 0,0,0）**：所有公式和计算
- **绿色文字（RGB: 0,128,0）**：同一工作簿内其他工作表的链接
- **红色文字（RGB: 255,0,0）**：指向其他文件的外部链接
- **黄色背景（RGB: 255,255,0）**：需要注意的关键假设或需要更新的单元格

### 数字格式标准

#### 格式规则
- **年份**：格式化为文本字符串（如 "2024" 而非 "2,024"）
- **货币**：使用 ¥#,##0 格式；始终在标题中指定单位（"收入（万元）"）
- **零值**：使用数字格式将所有零显示为 "-"
- **百分比**：默认 0.0% 格式（一位小数）
- **负数**：使用括号 (123) 而非减号 -123

### 公式构建规则

#### 假设放置
- 将所有假设（增长率、利润率、倍数等）放在单独的假设单元格中
- 在公式中使用单元格引用而非硬编码值
- 示例：使用 =B5*(1+$B$6) 而非 =B5*1.05

#### 公式错误预防
- 验证所有单元格引用正确
- 检查范围中的偏移错误
- 确保所有预测期公式一致
- 用边缘情况测试（零值、负数）
- 验证无意外循环引用

---

## 读取和分析数据

### 使用 pandas 进行数据分析

```python
import pandas as pd

# 读取 Excel
df = pd.read_excel('file.xlsx')  # 默认：第一个工作表
all_sheets = pd.read_excel('file.xlsx', sheet_name=None)  # 所有工作表作为字典

# 分析
df.head()      # 预览数据
df.info()      # 列信息
df.describe()  # 统计信息

# 写入 Excel
df.to_excel('output.xlsx', index=False)
```

## Excel 文件工作流程

## 关键：使用公式，不要硬编码值

**始终使用 Excel 公式，而非在 Python 中计算后硬编码值。** 这确保电子表格保持动态和可更新。

### ❌ 错误 - 硬编码计算值
```python
# 错误：在 Python 中计算并硬编码结果
total = df['Sales'].sum()
sheet['B10'] = total  # 硬编码 5000

# 错误：在 Python 中计算增长率
growth = (df.iloc[-1]['Revenue'] - df.iloc[0]['Revenue']) / df.iloc[0]['Revenue']
sheet['C5'] = growth  # 硬编码 0.15
```

### ✅ 正确 - 使用 Excel 公式
```python
# 正确：让 Excel 计算总和
sheet['B10'] = '=SUM(B2:B9)'

# 正确：增长率作为 Excel 公式
sheet['C5'] = '=(C4-C2)/C2'

# 正确：使用 Excel 函数计算平均值
sheet['D20'] = '=AVERAGE(D2:D19)'
```

## 常见工作流程
1. **选择工具**：pandas 用于数据，openpyxl 用于公式/格式
2. **创建/加载**：创建新工作簿或加载现有文件
3. **修改**：添加/编辑数据、公式和格式
4. **保存**：写入文件
5. **重算公式（使用公式时必须）**：使用 recalc.py 脚本
   ```bash
   python scripts/recalc.py output.xlsx
   ```
6. **验证并修复错误**：
   - 脚本返回包含错误详情的 JSON
   - 如果 `status` 是 `errors_found`，检查 `error_summary` 获取具体错误类型和位置
   - 修复错误并再次重算

### 创建新的 Excel 文件

```python
from openpyxl import Workbook
from openpyxl.styles import Font, PatternFill, Alignment

wb = Workbook()
sheet = wb.active

# 添加数据
sheet['A1'] = '你好'
sheet['B1'] = '世界'
sheet.append(['一行', '数据'])

# 添加公式
sheet['B2'] = '=SUM(A1:A10)'

# 格式化
sheet['A1'].font = Font(bold=True, color='FF0000')
sheet['A1'].fill = PatternFill('solid', start_color='FFFF00')
sheet['A1'].alignment = Alignment(horizontal='center')

# 列宽
sheet.column_dimensions['A'].width = 20

wb.save('output.xlsx')
```

### 编辑现有 Excel 文件

```python
from openpyxl import load_workbook

# 加载现有文件
wb = load_workbook('existing.xlsx')
sheet = wb.active  # 或 wb['SheetName']

# 处理多个工作表
for sheet_name in wb.sheetnames:
    sheet = wb[sheet_name]
    print(f"工作表：{sheet_name}")

# 修改单元格
sheet['A1'] = '新值'
sheet.insert_rows(2)  # 在位置 2 插入行
sheet.delete_cols(3)  # 删除第 3 列

# 添加新工作表
new_sheet = wb.create_sheet('新工作表')
new_sheet['A1'] = '数据'

wb.save('modified.xlsx')
```

## 重算公式

openpyxl 创建或修改的 Excel 文件包含公式字符串但没有计算值。使用 recalc.py 脚本重算：

```bash
python scripts/recalc.py <excel_file> [timeout_seconds]
```

脚本会：
- 自动设置 LibreOffice 宏
- 重算所有工作表中的所有公式
- 扫描所有单元格的 Excel 错误
- 返回包含详细错误位置和计数的 JSON

## 公式验证清单

### 基本验证
- **测试 2-3 个样本引用**：在构建完整模型前验证它们拉取正确值
- **列映射**：确认 Excel 列匹配
- **行偏移**：记住 Excel 行是 1 索引的（DataFrame 第 5 行 = Excel 第 6 行）

### 常见陷阱
- **NaN 处理**：使用 `pd.notna()` 检查空值
- **除零错误**：在使用 `/` 前检查分母
- **错误引用**：验证所有单元格引用指向目标单元格
- **跨表引用**：使用正确格式（Sheet1!A1）

### 解释 recalc.py 输出
```json
{
  "status": "success",
  "total_errors": 0,
  "total_formulas": 42,
  "error_summary": {
    "#REF!": {
      "count": 2,
      "locations": ["Sheet1!B5", "Sheet1!C10"]
    }
  }
}
```

## 最佳实践

### 库选择
- **pandas**：最适合数据分析、批量操作和简单数据导出
- **openpyxl**：最适合复杂格式、公式和 Excel 特定功能

### 使用 openpyxl
- 单元格索引从 1 开始（row=1, column=1 指 A1）
- 使用 `data_only=True` 读取计算值：`load_workbook('file.xlsx', data_only=True)`
- **警告**：如果以 `data_only=True` 打开并保存，公式将被永久替换为值
- 大文件：使用 `read_only=True` 读取或 `write_only=True` 写入

### 使用 pandas
- 指定数据类型避免推断问题：`pd.read_excel('file.xlsx', dtype={'id': str})`
- 大文件读取特定列：`pd.read_excel('file.xlsx', usecols=['A', 'C', 'E'])`
- 正确处理日期：`pd.read_excel('file.xlsx', parse_dates=['date_column'])`

## 代码风格
- 编写简洁的 Python 代码，无需不必要的注释
- 避免冗长的变量名和冗余操作
- 为复杂公式或重要假设添加单元格注释
- 记录硬编码值的数据来源
