# 中文版 AI 技能集合

专为中文用户打造的 AI Agent 技能库，让 AI 更好地服务中国开发者。

## 技能列表

### 常用办公

| 技能 | 说明 | 适用场景 |
|------|------|----------|
| `docx-zh` | Word 文档处理 | 创建、编辑、分析 .docx 文件 |
| `pptx-zh` | PPT 演示文稿 | 制作专业的演示文稿、汇报材料 |
| `xlsx-zh` | Excel 电子表格 | 数据处理、公式计算、财务模型 |
| `pdf-zh` | PDF 文件处理 | 读取、合并、拆分、OCR 识别 |

### 工程开发

| 技能 | 说明 | 适用场景 |
|------|------|----------|
| `tdd-zh` | 测试驱动开发 | 红-绿-重构循环，垂直切片开发 |
| `diagnose-zh` | 调试诊断 | 复现→假设→检查→修复的严格流程 |
| `frontend-design-zh` | 前端界面设计 | 创建独特的 Web 界面、组件 |
| `canvas-design-zh` | 画布视觉艺术 | 制作海报、艺术作品、设计稿 |
| `algorithmic-art-zh` | 算法生成艺术 | 使用 p5.js 创建生成艺术 |

### 生产力工具

| 技能 | 说明 | 适用场景 |
|------|------|----------|
| `code-assistant` | 代码助手 | 智能代码修改，提供方案选择 |
| `caveman-zh` | 极简沟通 | 减少 75% token，简洁表达 |
| `grill-me-zh` | 深入追问 | 逐个解决决策树的每个分支 |
| `skill-creator-zh` | 技能创建器 | 创建、测试、优化新技能 |
| `find-skills-zh` | 查找技能 | 搜索和安装现有技能 |
| `theme-factory-zh` | 主题工厂 | 为作品应用专业主题样式 |

## 安装使用

### 方式一：直接复制

将技能文件夹复制到你的 skills 目录：

```bash
# Claude Code / opencode
~/.agents/skills/

# 或指定目录
/path/to/your/skills/
```

### 方式二：克隆仓库

```bash
git clone https://gitee.com/nicholas-super/skills.git
cp -r skills/* ~/.agents/skills/
```

## 技能特点

- **全中文界面**：所有提示、说明、输出均使用中文
- **本土化设计**：适配中国常用格式（A4 纸张、中文排版等）
- **智能交互**：代码修改提供方案选择，支持自动/手动运行
- **工程导向**：TDD、调试等工程实践技能
- **易于扩展**：可根据需求自定义和创建新技能

## 目录结构

```
skills/
├── code-assistant/        # 代码助手
├── docx-zh/              # Word 文档
├── pptx-zh/              # PPT 演示
├── xlsx-zh/              # Excel 表格
├── pdf-zh/               # PDF 处理
├── tdd-zh/               # 测试驱动开发
├── diagnose-zh/          # 调试诊断
├── frontend-design-zh/   # 前端设计
├── canvas-design-zh/     # 画布艺术
├── algorithmic-art-zh/   # 算法艺术
├── caveman-zh/           # 极简沟通
├── grill-me-zh/           # 深入追问
├── skill-creator-zh/     # 技能创建
├── find-skills-zh/       # 查找技能
├── theme-factory-zh/     # 主题工厂
├── README.md             # 中文说明
└── README.en.md          # English docs
```

## 贡献指南

1. Fork 本仓库
2. 新建 `feat_xxx` 分支
3. 提交代码
4. 新建 Pull Request

## 许可证

各技能遵循其原始许可证。

## 相关链接

- [Gitee 仓库](https://gitee.com/nicholas-super/skills)
- [GitHub 仓库](https://github.com/zcccc-gif/skills)（自动同步）
- [技能市场](https://skills.sh/)

## 致谢

感谢所有原版技能的开发者，本仓库在其基础上进行了中文本地化适配。