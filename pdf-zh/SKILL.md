---
name: pdf-zh
description: "当用户需要处理 PDF 文件时使用此技能。包括：读取或提取文本/表格、合并多个 PDF、拆分 PDF、旋转页面、添加水印、创建新 PDF、填写 PDF 表单、加密/解密 PDF、提取图片、对扫描 PDF 进行 OCR 使其可搜索。如果用户提及 .pdf 文件或需要生成 PDF，使用此技能。"
---

# PDF 处理指南

## 概述

本指南涵盖使用 Python 库和命令行工具进行 PDF 处理的基本操作。

## 快速开始

```python
from pypdf import PdfReader, PdfWriter

# 读取 PDF
reader = PdfReader("document.pdf")
print(f"页数：{len(reader.pages)}")

# 提取文本
text = ""
for page in reader.pages:
    text += page.extract_text()
```

## Python 库

### pypdf - 基本操作

#### 合并 PDF
```python
from pypdf import PdfWriter, PdfReader

writer = PdfWriter()
for pdf_file in ["doc1.pdf", "doc2.pdf", "doc3.pdf"]:
    reader = PdfReader(pdf_file)
    for page in reader.pages:
        writer.add_page(page)

with open("merged.pdf", "wb") as output:
    writer.write(output)
```

#### 拆分 PDF
```python
reader = PdfReader("input.pdf")
for i, page in enumerate(reader.pages):
    writer = PdfWriter()
    writer.add_page(page)
    with open(f"page_{i+1}.pdf", "wb") as output:
        writer.write(output)
```

#### 提取元数据
```python
reader = PdfReader("document.pdf")
meta = reader.metadata
print(f"标题：{meta.title}")
print(f"作者：{meta.author}")
print(f"主题：{meta.subject}")
print(f"创建者：{meta.creator}")
```

#### 旋转页面
```python
reader = PdfReader("input.pdf")
writer = PdfWriter()

page = reader.pages[0]
page.rotate(90)  # 顺时针旋转 90 度
writer.add_page(page)

with open("rotated.pdf", "wb") as output:
    writer.write(output)
```

### pdfplumber - 文本和表格提取

#### 提取文本（保留布局）
```python
import pdfplumber

with pdfplumber.open("document.pdf") as pdf:
    for page in pdf.pages:
        text = page.extract_text()
        print(text)
```

#### 提取表格
```python
with pdfplumber.open("document.pdf") as pdf:
    for i, page in enumerate(pdf.pages):
        tables = page.extract_tables()
        for j, table in enumerate(tables):
            print(f"第 {i+1} 页的表格 {j+1}：")
            for row in table:
                print(row)
```

#### 高级表格提取
```python
import pandas as pd

with pdfplumber.open("document.pdf") as pdf:
    all_tables = []
    for page in pdf.pages:
        tables = page.extract_tables()
        for table in tables:
            if table:
                df = pd.DataFrame(table[1:], columns=table[0])
                all_tables.append(df)

if all_tables:
    combined_df = pd.concat(all_tables, ignore_index=True)
    combined_df.to_excel("extracted_tables.xlsx", index=False)
```

### reportlab - 创建 PDF

#### 基本 PDF 创建
```python
from reportlab.lib.pagesizes import A4
from reportlab.pdfgen import canvas

c = canvas.Canvas("hello.pdf", pagesize=A4)
width, height = A4

# 添加文本
c.drawString(100, height - 100, "你好世界！")
c.drawString(100, height - 120, "这是使用 reportlab 创建的 PDF")

# 添加线条
c.line(100, height - 140, 400, height - 140)

# 保存
c.save()
```

#### 创建多页 PDF
```python
from reportlab.lib.pagesizes import A4
from reportlab.platypus import SimpleDocTemplate, Paragraph, Spacer, PageBreak
from reportlab.lib.styles import getSampleStyleSheet
from reportlab.pdfbase import pdfmetrics
from reportlab.pdfbase.ttfonts import TTFont

# 注册中文字体
pdfmetrics.registerFont(TTFont('SimSun', 'simsun.ttc'))

doc = SimpleDocTemplate("report.pdf", pagesize=A4)
styles = getSampleStyleSheet()

# 设置中文字体
styles['Normal'].fontName = 'SimSun'

story = []

# 添加内容
title = Paragraph("报告标题", styles['Title'])
story.append(title)
story.append(Spacer(1, 12))

body = Paragraph("这是报告的正文内容。" * 20, styles['Normal'])
story.append(body)
story.append(PageBreak())

# 第 2 页
story.append(Paragraph("第二页", styles['Heading1']))
story.append(Paragraph("第二页的内容", styles['Normal']))

# 构建 PDF
doc.build(story)
```

#### 上标和下标

**重要**：在 ReportLab PDF 中不要使用 Unicode 上下标字符。使用 ReportLab 的 XML 标记：
```python
from reportlab.platypus import Paragraph

# 下标：使用 <sub> 标签
chemical = Paragraph("H<sub>2</sub>O", styles['Normal'])

# 上标：使用 <super> 标签
squared = Paragraph("x<super>2</super> + y<super>2</super>", styles['Normal'])
```

## 命令行工具

### pdftotext (poppler-utils)
```bash
# 提取文本
pdftotext input.pdf output.txt

# 保留布局提取
pdftotext -layout input.pdf output.txt

# 提取特定页
pdftotext -f 1 -l 5 input.pdf output.txt  # 第 1-5 页
```

### qpdf
```bash
# 合并 PDF
qpdf --empty --pages file1.pdf file2.pdf -- merged.pdf

# 拆分页面
qpdf input.pdf --pages . 1-5 -- pages1-5.pdf
qpdf input.pdf --pages . 6-10 -- pages6-10.pdf

# 旋转页面
qpdf input.pdf output.pdf --rotate=+90:1  # 旋转第 1 页

# 移除密码
qpdf --password=mypassword --decrypt encrypted.pdf decrypted.pdf
```

## 常见任务

### 从扫描 PDF 提取文本
```python
# 需要：pip install pytesseract pdf2image
import pytesseract
from pdf2image import convert_from_path

# 将 PDF 转换为图片
images = convert_from_path('scanned.pdf')

# OCR 每页
text = ""
for i, image in enumerate(images):
    text += f"第 {i+1} 页：\n"
    text += pytesseract.image_to_string(image, lang='chi_sim')  # 中文识别
    text += "\n\n"

print(text)
```

### 添加水印
```python
from pypdf import PdfReader, PdfWriter

# 创建水印（或加载现有）
watermark = PdfReader("watermark.pdf").pages[0]

# 应用到所有页面
reader = PdfReader("document.pdf")
writer = PdfWriter()

for page in reader.pages:
    page.merge_page(watermark)
    writer.add_page(page)

with open("watermarked.pdf", "wb") as output:
    writer.write(output)
```

### 提取图片
```bash
# 使用 pdfimages (poppler-utils)
pdfimages -j input.pdf output_prefix

# 这会提取所有图片为 output_prefix-000.jpg 等
```

### 密码保护
```python
from pypdf import PdfReader, PdfWriter

reader = PdfReader("input.pdf")
writer = PdfWriter()

for page in reader.pages:
    writer.add_page(page)

# 添加密码
writer.encrypt("用户密码", "所有者密码")

with open("encrypted.pdf", "wb") as output:
    writer.write(output)
```

## 快速参考

| 任务 | 最佳工具 | 命令/代码 |
|------|-----------|--------------|
| 合并 PDF | pypdf | `writer.add_page(page)` |
| 拆分 PDF | pypdf | 每页一个文件 |
| 提取文本 | pdfplumber | `page.extract_text()` |
| 提取表格 | pdfplumber | `page.extract_tables()` |
| 创建 PDF | reportlab | Canvas 或 Platypus |
| 命令行合并 | qpdf | `qpdf --empty --pages ...` |
| OCR 扫描 PDF | pytesseract | 先转换为图片 |

## 依赖项

- `pip install pypdf` - 基本操作
- `pip install pdfplumber` - 文本/表格提取
- `pip install reportlab` - 创建 PDF
- `pip install pytesseract pdf2image` - OCR
- `pip install Pillow` - 图片处理
- Poppler (`pdftotext`, `pdfimages`, `pdftoppm`) - 命令行工具
