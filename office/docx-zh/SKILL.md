---
name: docx-zh
description: "当用户想要创建、读取、编辑或处理 Word 文档（.docx 文件）时使用此技能。触发条件包括：提及'Word文档'、'.docx'、或需要制作带有目录、标题、页眉页脚等专业格式的文档。也适用于从 .docx 文件中提取或重组内容、插入图片、查找替换、处理修订和批注、或将内容转换为精美的 Word 文档。如果用户需要'报告'、'备忘录'、'信函'、'模板'等以 Word 格式交付的文档，使用此技能。"
---

# DOCX 文档创建、编辑与分析

## 概述

.docx 文件是一个包含 XML 文件的 ZIP 压缩包。

## 快速参考

| 任务 | 方法 |
|------|------|
| 读取/分析内容 | `pandoc` 或解压获取原始 XML |
| 创建新文档 | 使用 `docx-js` - 参见下方"创建新文档" |
| 编辑现有文档 | 解压 → 编辑 XML → 重新打包 - 参见下方"编辑现有文档" |

### 转换 .doc 为 .docx

旧版 .doc 文件需要先转换：

```bash
python scripts/office/soffice.py --headless --convert-to docx document.doc
```

### 读取内容

```bash
# 提取文本（包含修订）
pandoc --track-changes=all document.docx -o output.md

# 访问原始 XML
python scripts/office/unpack.py document.docx unpacked/
```

### 转换为图片

```bash
python scripts/office/soffice.py --headless --convert-to pdf document.docx
pdftoppm -jpeg -r 150 document.pdf page
```

### 接受修订

要生成接受所有修订的干净文档（需要 LibreOffice）：

```bash
python scripts/accept_changes.py input.docx output.docx
```

---

## 创建新文档

使用 JavaScript 生成 .docx 文件，然后验证。安装：`npm install -g docx`

### 设置
```javascript
const { Document, Packer, Paragraph, TextRun, Table, TableRow, TableCell, ImageRun,
        Header, Footer, AlignmentType, PageOrientation, LevelFormat, ExternalHyperlink,
        InternalHyperlink, Bookmark, FootnoteReferenceRun, PositionalTab,
        PositionalTabAlignment, PositionalTabRelativeTo, PositionalTabLeader,
        TabStopType, TabStopPosition, Column, SectionType,
        TableOfContents, HeadingLevel, BorderStyle, WidthType, ShadingType,
        VerticalAlign, PageNumber, PageBreak } = require('docx');

const doc = new Document({ sections: [{ children: [/* 内容 */] }] });
Packer.toBuffer(doc).then(buffer => fs.writeFileSync("doc.docx", buffer));
```

### 验证
创建文件后进行验证。如果验证失败，解压、修复 XML、重新打包。
```bash
python scripts/office/validate.py doc.docx
```

### 页面大小

```javascript
// 重要：docx-js 默认使用 A4 纸张
// 中国标准为 A4（210mm × 297mm）
sections: [{
  properties: {
    page: {
      size: {
        width: 11906,   // A4 宽度（DXA）
        height: 16838   // A4 高度（DXA）
      },
      margin: { top: 1440, right: 1440, bottom: 1440, left: 1440 } // 1 英寸边距
    }
  },
  children: [/* 内容 */]
}]
```

**常用页面大小（DXA 单位，1440 DXA = 1 英寸）：**

| 纸张 | 宽度 | 高度 | 内容宽度（1英寸边距） |
|-------|-------|--------|---------------------------|
| A4（默认） | 11,906 | 16,838 | 9,026 |
| US Letter | 12,240 | 15,840 | 9,360 |

**横向布局：** docx-js 内部会交换宽高，所以传递纵向尺寸：
```javascript
size: {
  width: 11906,   // 传递短边作为宽度
  height: 16838,  // 传递长边作为高度
  orientation: PageOrientation.LANDSCAPE  // docx-js 会在 XML 中交换
},
```

### 样式（覆盖内置标题）

使用微软雅黑或宋体作为默认字体（中文文档常用）。标题使用黑色。

```javascript
const doc = new Document({
  styles: {
    default: { document: { run: { font: "微软雅黑", size: 24 } } }, // 12pt 默认
    paragraphStyles: [
      // 重要：使用精确的 ID 覆盖内置样式
      { id: "Heading1", name: "Heading 1", basedOn: "Normal", next: "Normal", quickFormat: true,
        run: { size: 32, bold: true, font: "微软雅黑" },
        paragraph: { spacing: { before: 240, after: 240 }, outlineLevel: 0 } },
      { id: "Heading2", name: "Heading 2", basedOn: "Normal", next: "Normal", quickFormat: true,
        run: { size: 28, bold: true, font: "微软雅黑" },
        paragraph: { spacing: { before: 180, after: 180 }, outlineLevel: 1 } },
    ]
  },
  sections: [{
    children: [
      new Paragraph({ heading: HeadingLevel.HEADING_1, children: [new TextRun("标题")] }),
    ]
  }]
});
```

### 列表（不要使用 unicode 符号）

```javascript
// ❌ 错误 - 不要手动插入符号字符
new Paragraph({ children: [new TextRun("• 项目")] })  // 错误

// ✅ 正确 - 使用 numbering 配置
const doc = new Document({
  numbering: {
    config: [
      { reference: "bullets",
        levels: [{ level: 0, format: LevelFormat.BULLET, text: "•", alignment: AlignmentType.LEFT,
          style: { paragraph: { indent: { left: 720, hanging: 360 } } } }] },
      { reference: "numbers",
        levels: [{ level: 0, format: LevelFormat.DECIMAL, text: "%1.", alignment: AlignmentType.LEFT,
          style: { paragraph: { indent: { left: 720, hanging: 360 } } } }] },
    ]
  },
  sections: [{
    children: [
      new Paragraph({ numbering: { reference: "bullets", level: 0 },
        children: [new TextRun("列表项")] }),
      new Paragraph({ numbering: { reference: "numbers", level: 0 },
        children: [new TextRun("编号项")] }),
    ]
  }]
});
```

### 表格

**重要：表格需要双重宽度设置** - 在表格上设置 `columnWidths` 并在每个单元格上设置 `width`。

```javascript
// 重要：始终设置表格宽度以确保一致的渲染
const border = { style: BorderStyle.SINGLE, size: 1, color: "CCCCCC" };
const borders = { top: border, bottom: border, left: border, right: border };

new Table({
  width: { size: 9026, type: WidthType.DXA }, // A4 内容宽度
  columnWidths: [4513, 4513], // 必须总和等于表格宽度
  rows: [
    new TableRow({
      children: [
        new TableCell({
          borders,
          width: { size: 4513, type: WidthType.DXA },
          shading: { fill: "D5E8F0", type: ShadingType.CLEAR },
          margins: { top: 80, bottom: 80, left: 120, right: 120 },
          children: [new Paragraph({ children: [new TextRun("单元格")] })]
        })
      ]
    })
  ]
})
```

### 图片

```javascript
// 重要：type 参数是必需的
new Paragraph({
  children: [new ImageRun({
    type: "png", // 必需：png, jpg, jpeg, gif, bmp, svg
    data: fs.readFileSync("image.png"),
    transformation: { width: 200, height: 150 },
    altText: { title: "标题", description: "描述", name: "名称" }
  })]
})
```

### 分页符

```javascript
// 重要：PageBreak 必须在 Paragraph 内
new Paragraph({ children: [new PageBreak()] })

// 或使用 pageBreakBefore
new Paragraph({ pageBreakBefore: true, children: [new TextRun("新页面")] })
```

### 超链接

```javascript
// 外部链接
new Paragraph({
  children: [new ExternalHyperlink({
    children: [new TextRun({ text: "点击这里", style: "Hyperlink" })],
    link: "https://example.com",
  })]
})

// 内部链接（书签 + 引用）
new Paragraph({ heading: HeadingLevel.HEADING_1, children: [
  new Bookmark({ id: "chapter1", children: [new TextRun("第一章")] }),
]})
new Paragraph({ children: [new InternalHyperlink({
  children: [new TextRun({ text: "参见第一章", style: "Hyperlink" })],
  anchor: "chapter1",
})]})
```

### 脚注

```javascript
const doc = new Document({
  footnotes: {
    1: { children: [new Paragraph("来源：2024年年度报告")] },
    2: { children: [new Paragraph("详见附录中的方法说明")] },
  },
  sections: [{
    children: [new Paragraph({
      children: [
        new TextRun("收入增长了15%"),
        new FootnoteReferenceRun(1),
        new TextRun("（使用调整后的指标）"),
        new FootnoteReferenceRun(2),
      ],
    })]
  }]
});
```

### 目录

```javascript
// 重要：标题必须仅使用 HeadingLevel - 不要使用自定义样式
new TableOfContents("目录", { hyperlink: true, headingStyleRange: "1-3" })
```

### 页眉/页脚

```javascript
sections: [{
  properties: {
    page: { margin: { top: 1440, right: 1440, bottom: 1440, left: 1440 } }
  },
  headers: {
    default: new Header({ children: [new Paragraph({ children: [new TextRun("页眉")] })] })
  },
  footers: {
    default: new Footer({ children: [new Paragraph({
      children: [new TextRun("第 "), new TextRun({ children: [PageNumber.CURRENT] }), new TextRun(" 页")]
    })] })
  },
  children: [/* 内容 */]
}]
```

### docx-js 关键规则

- **显式设置页面大小** - docx-js 默认 A4，适合中国标准
- **横向布局：传递纵向尺寸** - docx-js 内部交换宽高
- **不要使用 `\n`** - 使用单独的 Paragraph 元素
- **不要使用 unicode 符号** - 使用 `LevelFormat.BULLET`
- **PageBreak 必须在 Paragraph 内**
- **ImageRun 需要 `type`** - 始终指定 png/jpg 等
- **始终使用 DXA 设置表格宽度** - 不要使用 `WidthType.PERCENTAGE`
- **表格需要双重宽度** - `columnWidths` 数组和单元格 `width` 必须匹配
- **使用 `ShadingType.CLEAR`** - 不要使用 SOLID
- **目录仅支持 HeadingLevel** - 不要在标题段落上使用自定义样式

---

## 编辑现有文档

**按顺序执行以下 3 个步骤。**

### 步骤 1：解压
```bash
python scripts/office/unpack.py document.docx unpacked/
```

### 步骤 2：编辑 XML

编辑 `unpacked/word/` 中的文件。使用 Edit 工具直接进行字符串替换，不要编写 Python 脚本。

**使用中文引号：** 添加带引号的文本时，使用中文引号：
```xml
<w:t>他说：&#x201C;你好&#x201D;</w:t>
```

### 步骤 3：打包
```bash
python scripts/office/pack.py unpacked/ output.docx --original document.docx
```

---

## 依赖项

- **pandoc**：文本提取
- **docx**：`npm install -g docx`（创建新文档）
- **LibreOffice**：PDF 转换
- **Poppler**：`pdftoppm` 用于图片
