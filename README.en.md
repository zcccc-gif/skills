# Chinese AI Skills Collection

AI Agent skills designed for Chinese users, making AI work better for developers in China.

---

## Quick Start

Just describe your needs in the conversation, and AI will automatically match relevant skills:
- "帮我把这个函数改个名字" (Help me rename this function)
- "原始人模式，简洁点" (Caveman mode, be brief)
- "用 tdd 写这个功能" (Use TDD to write this feature)
- "帮我诊断一下这个 bug" (Help me diagnose this bug)

---

## Skills Categories

### 1. Code Assistant `code-assistant/`

| Skill | Description | Trigger Keywords |
|-------|-------------|------------------|
| `code-assistant` | Provide plan before modifying code, execute after user confirms | "修改代码", "重构", "优化" |
| `tdd-zh` | Test-driven development with red-green-refactor loop | "tdd", "红绿重构", "测试优先" |
| `diagnose-zh` | Strict debugging process | "诊断", "调试", "debug" |

### 2. Communication `communication/`

| Skill | Description | Trigger Keywords |
|-------|-------------|------------------|
| `caveman-zh` | Ultra-compressed mode, 75% token reduction | "原始人模式", "简洁点" |
| `grill-me-zh` | Deep interrogation until all decisions are clarified | "追问", "压力测试" |

### 3. Office `office/`

| Skill | Description | Trigger Keywords |
|-------|-------------|------------------|
| `docx-zh` | Word document creation and editing | "word", "文档" |
| `pptx-zh` | PowerPoint presentation | "ppt", "演示", "幻灯片" |
| `xlsx-zh` | Excel spreadsheet processing | "excel", "表格" |
| `pdf-zh` | PDF file processing | "pdf" |

### 4. Design `design/`

| Skill | Description | Trigger Keywords |
|-------|-------------|------------------|
| `frontend-design-zh` | Web interface design | "前端", "网页", "界面" |
| `canvas-design-zh` | Canvas visual art | "海报", "艺术", "设计" |
| `algorithmic-art-zh` | Algorithmic generative art | "算法艺术", "生成艺术" |

### 5. Tools `tools/`

| Skill | Description | Trigger Keywords |
|-------|-------------|------------------|
| `skill-creator-zh` | Create and test new skills | "创建技能", "新建技能" |
| `find-skills-zh` | Search and install existing skills | "找技能", "搜索skill" |
| `theme-factory-zh` | Apply professional theme styles | "主题", "配色" |

---

## Directory Structure

```
skills/
├── code-assistant/           # Code Assistant Category
│   ├── code-assistant/      # Smart code modification
│   ├── tdd-zh/             # Test-Driven Development
│   ├── diagnose-zh/         # Debugging & Diagnosis
│   └── README.md
├── communication/           # Communication Category
│   ├── caveman-zh/         # Ultra-compressed Mode
│   ├── grill-me-zh/        # Deep Interrogation
│   └── README.md
├── office/                  # Office Category
│   ├── docx-zh/            # Word Documents
│   ├── pptx-zh/            # PowerPoint
│   ├── xlsx-zh/            # Excel
│   ├── pdf-zh/             # PDF
│   └── README.md
├── design/                  # Design Category
│   ├── frontend-design-zh/ # Frontend Design
│   ├── canvas-design-zh/   # Canvas Art
│   ├── algorithmic-art-zh/  # Algorithmic Art
│   └── README.md
├── tools/                   # Tools Category
│   ├── skill-creator-zh/   # Skill Creator
│   ├── find-skills-zh/     # Find Skills
│   ├── theme-factory-zh/   # Theme Factory
│   └── README.md
├── README.md               # This file
└── README.en.md            # English version
```

---

## Installation

### Local Installation

Copy skill folders to your skills directory:

```bash
# Claude Code / opencode
~/.agents/skills/

# Windows
C:/Users/your-username/.agents/skills/
```

### Remote Installation

```bash
git clone https://gitee.com/nicholas-super/skills.git
cp -r skills/* ~/.agents/skills/
```

---

## Links

- [Gitee Repository](https://gitee.com/nicholas-super/skills)
- [GitHub Repository](https://github.com/zcccc-gif/skills) (auto-sync)
- [Skills Marketplace](https://skills.sh/)

---

## Acknowledgments

Thanks to all original skill developers. This repository provides Chinese localization based on their work.

Inspired by: [mattpocock/skills](https://github.com/mattpocock/skills)
