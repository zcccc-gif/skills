# 中文版 AI 技能集合

专为中文用户打造的 AI Agent 技能库，让 AI 更好地服务中国开发者。

---

## 快速开始

在对话中直接说出你的需求，AI 会自动匹配相关技能。例如：
- "帮我把这个函数改个名字"
- "原始人模式，简洁点"
- "用 tdd 写这个功能"
- "帮我诊断一下这个 bug"

---

## 技能分类

### 1. 代码助手类 `code-assistant/`

| 技能 | 说明 | 触发关键词 |
|------|------|-----------|
| `code-assistant` | 修改代码前先给方案，用户确认后再执行 | "修改代码"、"重构"、"优化" |
| `tdd-zh` | 测试驱动开发，红-绿-重构循环 | "tdd"、"红绿重构"、"测试优先" |
| `diagnose-zh` | 严格的调试流程 | "诊断"、"调试"、"debug" |

### 2. 沟通效率类 `communication/`

| 技能 | 说明 | 触发关键词 |
|------|------|-----------|
| `caveman-zh` | 极简沟通，减少 75% token | "原始人模式"、"简洁点" |
| `grill-me-zh` | 深入追问直到所有决策明确 | "追问"、"压力测试" |

### 3. 办公文档类 `office/`

| 技能 | 说明 | 触发关键词 |
|------|------|-----------|
| `docx-zh` | Word 文档创建、编辑 | "word"、"文档" |
| `pptx-zh` | PPT 演示文稿制作 | "ppt"、"演示"、"幻灯片" |
| `xlsx-zh` | Excel 电子表格处理 | "excel"、"表格" |
| `pdf-zh` | PDF 文件处理 | "pdf" |

### 4. 设计创意类 `design/`

| 技能 | 说明 | 触发关键词 |
|------|------|-----------|
| `frontend-design-zh` | Web 界面设计 | "前端"、"网页"、"界面" |
| `canvas-design-zh` | 画布视觉艺术 | "海报"、"艺术"、"设计" |
| `algorithmic-art-zh` | 算法生成艺术 | "算法艺术"、"生成艺术" |

### 5. 工具类 `tools/`

| 技能 | 说明 | 触发关键词 |
|------|------|-----------|
| `skill-creator-zh` | 创建和测试新技能 | "创建技能"、"新建技能" |
| `find-skills-zh` | 搜索和安装现有技能 | "找技能"、"搜索skill" |
| `theme-factory-zh` | 应用专业主题样式 | "主题"、"配色" |

---

## 目录结构

```
skills/
├── code-assistant/           # 代码助手类
│   ├── code-assistant/      # 智能代码修改
│   ├── tdd-zh/             # 测试驱动开发
│   ├── diagnose-zh/         # 调试诊断
│   └── README.md
├── communication/           # 沟通效率类
│   ├── caveman-zh/         # 极简沟通
│   ├── grill-me-zh/         # 深入追问
│   └── README.md
├── office/                  # 办公文档类
│   ├── docx-zh/            # Word 文档
│   ├── pptx-zh/            # PPT 演示
│   ├── xlsx-zh/            # Excel 表格
│   ├── pdf-zh/             # PDF 处理
│   └── README.md
├── design/                  # 设计创意类
│   ├── frontend-design-zh/ # 前端设计
│   ├── canvas-design-zh/   # 画布艺术
│   ├── algorithmic-art-zh/  # 算法艺术
│   └── README.md
├── tools/                   # 工具类
│   ├── skill-creator-zh/   # 技能创建
│   ├── find-skills-zh/     # 查找技能
│   ├── theme-factory-zh/   # 主题工厂
│   └── README.md
├── README.md               # 本文件
└── README.en.md            # English version
```

---

## 安装使用

### 本地安装

将技能文件夹复制到你的 skills 目录：

```bash
# Claude Code / opencode
~/.agents/skills/

# Windows
C:/Users/你的用户名/.agents/skills/
```

### 远程安装

```bash
git clone https://gitee.com/nicholas-super/skills.git
cp -r skills/* ~/.agents/skills/
```

---

## 相关链接

- [Gitee 仓库](https://gitee.com/nicholas-super/skills)
- [GitHub 仓库](https://github.com/zcccc-gif/skills)（自动同步）
- [技能市场](https://skills.sh/)

---

## 致谢

感谢所有原版技能的开发者，本仓库在其基础上进行了中文本地化适配。

灵感来源：[mattpocock/skills](https://github.com/mattpocock/skills)
