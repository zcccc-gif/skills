# Chinese AI Skills Collection

AI Agent skills designed for Chinese users, making AI work better for developers in China.

## Skills List

### Office

| Skill | Description | Use Cases |
|-------|-------------|-----------|
| `docx-zh` | Word Document | Create, edit, analyze .docx files |
| `pptx-zh` | PowerPoint | Professional presentations and reports |
| `xlsx-zh` | Excel Spreadsheet | Data processing, formulas, financial models |
| `pdf-zh` | PDF Processing | Read, merge, split, OCR recognition |

### Engineering

| Skill | Description | Use Cases |
|-------|-------------|-----------|
| `tdd-zh` | Test-Driven Development | Red-green-refactor loop, vertical slices |
| `diagnose-zh` | Debugging & Diagnosis | Reproduce→hypothesize→instrument→fix loop |
| `frontend-design-zh` | Frontend Design | Create unique web interfaces and components |
| `canvas-design-zh` | Canvas Art | Posters, artwork, design drafts |
| `algorithmic-art-zh` | Algorithmic Art | Generative art with p5.js |

### Productivity

| Skill | Description | Use Cases |
|-------|-------------|-----------|
| `code-assistant` | Code Assistant | Smart code modification with options |
| `caveman-zh` | Ultra-compressed Mode | 75% token reduction, brief communication |
| `grill-me-zh` | Deep Interrogation | Resolve every branch of decision tree |
| `skill-creator-zh` | Skill Creator | Create, test, optimize new skills |
| `find-skills-zh` | Find Skills | Search and install existing skills |
| `theme-factory-zh` | Theme Factory | Apply professional themes to artifacts |

## Installation

### Option 1: Copy Directly

Copy skill folders to your skills directory:

```bash
# Claude Code / opencode
~/.agents/skills/

# Or custom directory
/path/to/your/skills/
```

### Option 2: Clone Repository

```bash
git clone https://gitee.com/nicholas-super/skills.git
cp -r skills/* ~/.agents/skills/
```

## Features

- **Full Chinese Interface**: All prompts, instructions, and outputs in Chinese
- **Localized Design**: Adapted for Chinese formats (A4 paper, Chinese typography, etc.)
- **Smart Interaction**: Code modification provides options, supports auto/manual execution
- **Engineering-Oriented**: TDD, debugging, and engineering practice skills
- **Easy to Extend**: Customize and create new skills as needed

## Directory Structure

```
skills/
├── code-assistant/        # Code Assistant
├── docx-zh/              # Word Document
├── pptx-zh/              # PowerPoint
├── xlsx-zh/              # Excel Spreadsheet
├── pdf-zh/               # PDF Processing
├── tdd-zh/               # Test-Driven Development
├── diagnose-zh/          # Debugging & Diagnosis
├── frontend-design-zh/   # Frontend Design
├── canvas-design-zh/     # Canvas Art
├── algorithmic-art-zh/   # Algorithmic Art
├── caveman-zh/           # Ultra-compressed Mode
├── grill-me-zh/          # Deep Interrogation
├── skill-creator-zh/     # Skill Creator
├── find-skills-zh/       # Find Skills
├── theme-factory-zh/     # Theme Factory
├── README.md             # Chinese Docs
└── README.en.md          # English Docs
```

## Contribution

1. Fork the repository
2. Create `feat_xxx` branch
3. Commit your code
4. Create Pull Request

## License

Each skill follows its original license.

## Links

- [Gitee Repository](https://gitee.com/nicholas-super/skills)
- [GitHub Repository](https://github.com/zcccc-gif/skills) (auto-sync)
- [Skills Marketplace](https://skills.sh/)

## Acknowledgments

Thanks to all original skill developers. This repository provides Chinese localization based on their work.