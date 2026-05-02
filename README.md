# 中文版 AI 技能集合

专为中文用户打造的 AI Agent 技能库，让 AI 更好地服务中国开发者。

## 快速开始

在对话中直接说出你的需求，AI 会自动匹配相关技能。例如：
- "帮我把这个函数改个名字"
- "简洁点说"
- "追问一下我的方案"
- "用 tdd 写这个功能"

---

## 技能分类与触发条件

### 代码助手类

| 技能 | 触发关键词 | 说明 |
|------|-----------|------|
| `chinese-code-modify` | "修改代码"、"重构"、"优化代码"、"改函数名"、"修复bug" | 修改代码前先给方案，用户确认后再执行 |
| `tdd-zh` | "tdd"、"红绿重构"、"测试优先"、"用TDD" | 测试驱动开发，垂直切片开发 |
| `diagnose-zh` | "诊断"、"调试"、"debug"、"找出bug" | 严格的调试流程：复现→假设→检查→修复 |

**代码助手类用法示例：**
- "帮我把 calc() 函数改名叫 calculate_total_price()"
  → AI 会给出修改方案，列出步骤和可能结果，让你选择后再执行
- "用 tdd 写一个用户登录功能"
  → AI 会先写测试，再写代码，循环直到完成
- "程序报错了，帮我诊断一下"
  → AI 会引导你复现问题、提出假设、验证修复

### 沟通效率类

| 技能 | 触发关键词 | 说明 |
|------|-----------|------|
| `caveman-zh` | "原始人模式"、"简洁点"、"少用token"、"caveman" | 压缩表达，减少 75% token |
| `grill-me-zh` | "追问"、"压力测试"、"深入提问"、"grill" | 深入追问直到所有决策明确 |

**沟通效率类用法示例：**
- "原始人模式" → AI 开始极简回复，删掉所有废话
- "追问一下我的登录方案" → AI 逐个问题深入提问，确保考虑周全

### 办公文档类

| 技能 | 触发关键词 | 说明 |
|------|-----------|------|
| `docx-zh` | "word"、"docx"、"文档"、"创建文档" | 创建、编辑 Word 文档 |
| `pptx-zh` | "ppt"、"演示"、"幻灯片"、"presentation" | 创建、编辑 PPT |
| `xlsx-zh` | "excel"、"表格"、"xlsx"、"电子表格" | 创建、编辑 Excel |
| `pdf-zh` | "pdf"、"转换pdf"、"读取pdf" | PDF 处理、合并、拆分、OCR |

### 设计创意类

| 技能 | 触发关键词 | 说明 |
|------|-----------|------|
| `frontend-design-zh` | "前端"、"网页"、"界面设计"、"web组件" | 创建独特的 Web 界面 |
| `canvas-design-zh` | "海报"、"艺术"、"设计"、"画布" | 创建视觉艺术作品 |
| `algorithmic-art-zh` | "算法艺术"、"生成艺术"、"p5.js" | 创建代码生成的艺术 |

### 工具类

| 技能 | 触发关键词 | 说明 |
|------|-----------|------|
| `skill-creator-zh` | "创建技能"、"写一个skill"、"新建技能" | 创建和测试新技能 |
| `find-skills-zh` | "找技能"、"搜索skill"、"有没有技能" | 搜索和安装现有技能 |
| `theme-factory-zh` | "主题"、"配色"、"样式"、"theme" | 应用专业主题样式 |

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

## 目录结构

```
skills/
├── chinese-code-modify/    # 代码助手（方案+确认模式）
├── tdd-zh/                 # 测试驱动开发
├── diagnose-zh/            # 调试诊断
├── caveman-zh/             # 极简沟通
├── grill-me-zh/            # 深入追问
├── docx-zh/                # Word 文档
├── pptx-zh/                # PPT 演示
├── xlsx-zh/                # Excel 表格
├── pdf-zh/                 # PDF 处理
├── frontend-design-zh/     # 前端设计
├── canvas-design-zh/       # 画布艺术
├── algorithmic-art-zh/     # 算法艺术
├── skill-creator-zz/       # 技能创建
├── find-skills-zh/         # 查找技能
├── theme-factory-zh/       # 主题工厂
└── README.md
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
