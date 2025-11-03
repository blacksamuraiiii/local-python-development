# Local Python Development Plugin

一个基于 [wshobson/agents](https://github.com/wshobson/agents) 中 python-development 改进的本地Python开发插件，专为现代Python开发工作流程设计，集成了Streamlit、CustomTkinter和Conda环境管理。

## 🚀 项目概述

本项目是一个Claude插件，提供了全面的Python开发支持，包括Web应用开发、桌面GUI应用开发、异步编程模式以及现代化的包管理。通过智能代理和技能系统，为Python开发者提供场景驱动的开发体验。

## ✨ 主要特性

### 🎯 智能代理系统
- **python-pro**: Python 3.12+ 现代开发专家，掌握最新工具和最佳实践
- **streamlit-pro**: Streamlit应用开发专家，专注于数据仪表板和交互式Web应用
- **tkinter-pro**: CustomTkinter GUI开发专家，构建现代化桌面应用程序
- **django-pro**: Django 5.x 全栈Web应用开发专家
- **fastapi-pro**: 高性能异步API开发专家

### 🛠️ 专业技能模块
- **async-python-patterns**: 异步编程模式和并发系统
- **conda-pip-management**: Conda环境与pip包管理
- **python-packaging**: Python应用打包和分发
- **python-performance-optimization**: 性能分析和优化
- **python-testing-patterns**: 测试驱动开发和质量保证
- **uv-package-manager**: 现代包管理工具uv

### 📋 项目脚手架
- **python-scaffold**: 自动化Python项目结构生成
- 支持Streamlit应用、CustomTkinter GUI、Python库、CLI工具等多种项目类型
- 集成Conda环境管理和现代开发工具配置

## 📁 项目结构

```
local-python-development/
├── CLAUDE.md                    # Python开发工作规则和智能触发规则
├── README.md                    # 项目说明文档
├── .claude-plugin/              # Claude插件配置
│   ├── marketplace.json         # 插件市场配置
│   └── plugin.json              # 插件元数据
├── agents/                      # 智能代理
│   ├── python-pro.md            # Python开发专家
│   ├── streamlit-pro.md         # Streamlit应用专家
│   ├── tkinter-pro.md           # CustomTkinter GUI专家
│   ├── django-pro.md            # Django全栈开发专家
│   └── fastapi-pro.md           # FastAPI异步API专家
├── commands/                    # 命令工具
│   └── python-scaffold.md       # Python项目脚手架
└── skills/                      # 技能模块
    ├── async-python-patterns/   # 异步编程模式
    ├── conda-pip-management/     # Conda与pip包管理
    ├── python-packaging/        # Python应用打包
    ├── python-performance-optimization/ # 性能优化
    ├── python-testing-patterns/ # 测试模式
    └── uv-package-manager/      # UV包管理器
```

## 🎮 使用方法

### 安装插件

1. 将此项目克隆到Claude插件目录：
```bash
git clone <repository-url> ~/.claude/plugins/local-python-development
```

2. 复制CLAUDE.md到Claude配置目录：
```bash
cp ~/.claude/plugins/local-python-development/CLAUDE.md ~/.claude/CLAUDE.md
```

3. 重启Claude以加载插件

### 配置说明

#### 插件目录结构
Claude会自动识别以下目录结构中的代理和技能：
```
~/.claude/plugins/local-python-development/
├── agents/          # 智能代理文件 (*.md)
├── skills/          # 技能模块 (目录/SKILL.md)
├── commands/        # 命令工具 (*.md)
└── .claude-plugin/  # 插件配置
    └── plugin.json
```

#### 代理和技能自动发现
- **代理**: 放置在 `agents/` 目录下的 `.md` 文件，包含YAML前置元数据
- **技能**: 放置在 `skills/` 目录下的子目录，每个子目录包含 `SKILL.md` 文件
- **命令**: 放置在 `commands/` 目录下的 `.md` 文件

#### CLAUDE.md配置
`CLAUDE.md` 文件定义了智能触发规则，根据关键词自动选择合适的代理和技能：

- 提及"streamlit"、"仪表板" → 自动调用 `streamlit-pro`
- 提及"tkinter"、"GUI" → 自动调用 `tkinter-pro`
- 提及"conda"、"pip" → 自动调用 `conda-pip-management`
- 提及"异步"、"async" → 自动调用 `async-python-patterns`

#### 可选：Claude设置文件
在 `~/.claude/settings.json` 中可以添加额外配置：

```json
{
  "extraKnownMarketplaces": [
    {
      "name": "local-python-development",
      "url": "https://github.com/your-org/local-python-development"
    }
  ],
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp"]
    }
  }
}
```

### 智能触发

插件会根据您的开发需求自动选择合适的代理和技能：

#### Web应用开发
- 提及"streamlit"、"仪表板"、"数据可视化" → 自动调用 `streamlit-pro`
- 提及"django"、"全栈应用" → 自动调用 `django-pro`
- 提及"fastapi"、"异步API" → 自动调用 `fastapi-pro`

#### 桌面应用开发
- 提及"tkinter"、"GUI"、"桌面应用" → 自动调用 `tkinter-pro`

#### 通用Python开发
- 提及"python"、"异步编程" → 自动调用 `python-pro` + `async-python-patterns`
- 提及"性能优化" → 自动调用 `python-pro` + `python-performance-optimization`
- 提及"测试" → 自动调用 `python-pro` + `python-testing-patterns`

#### 环境和包管理
- 提及"conda"、"pip"、"包管理" → 自动调用 `conda-pip-management`
- 提及"打包"、"PyInstaller" → 自动调用 `python-packaging`

### 项目脚手架使用

创建新的Streamlit应用：
```
使用python-scaffold创建一个名为"数据仪表板"的Streamlit应用
```

创建新的CustomTkinter GUI应用：
```
使用python-scaffold创建一个名为"系统工具"的CustomTkinter桌面应用
```

## 🔧 核心改进

### 新增组件

1. **streamlit-pro.md**
   - 专门针对Streamlit 1.28+最新特性
   - 包含认证系统、缓存策略、状态管理
   - 生产部署和性能优化最佳实践

2. **tkinter-pro.md**
   - 专注于CustomTkinter现代UI开发
   - 响应式设计和多线程处理
   - 应用打包和分发准备

3. **conda-pip-management技能**
   - 全面的Conda环境管理指南
   - 混合工作流（Conda + pip）最佳实践
   - 数据科学和机器学习环境配置

### 增强功能

- **智能触发规则**: 根据关键词自动选择合适的代理和技能组合
- **场景驱动开发**: 针对不同开发场景提供专门的工作流程
- **现代工具集成**: 支持uv、ruff、mypy等2024/2025最新工具
- **生产就绪**: 强调测试、部署、监控等生产环境考虑

## 🎯 开发场景

### 数据科学项目
```python
# 自动触发: streamlit-pro + conda-pip-management
创建一个交互式数据仪表板，使用Streamlit展示数据分析结果
```

### 桌面工具开发
```python
# 自动触发: tkinter-pro + python-packaging
开发一个数据处理的桌面应用，使用CustomTkinter构建现代化界面
```

### 异步API服务
```python
# 自动触发: fastapi-pro + async-python-patterns
构建高性能异步API，支持WebSocket和实时数据更新
```

### 性能优化项目
```python
# 自动触发: python-pro + python-performance-optimization
优化现有Python应用的性能，分析瓶颈并实施改进
```

## 🛠️ 环境要求

- Python 3.11+
- Conda/Miniconda
- Claude Desktop应用
- 推荐使用现代IDE（VS Code、PyCharm）

## 📚 文档和资源

- [CLAUDE.md](./CLAUDE.md) - 详细的开发规则和触发逻辑
- [agents/](./agents/) - 各个代理的详细能力说明
- [skills/](./skills/) - 技能模块的专业指南
- [commands/](./commands/) - 可用命令的使用说明

## 🤝 贡献指南

欢迎提交Issue和Pull Request来改进这个插件！

### 开发环境设置

1. 克隆项目
2. 创建Conda环境：`conda env create -f environment.yml`
3. 激活环境：`conda activate local-python-dev`
4. 安装开发依赖：`pip install -e .`

### 提交规范

- 使用清晰的提交信息
- 为新功能添加文档
- 确保所有代理和技能遵循统一的格式规范

## 📄 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

## 🙏 致谢

- 基于 [wshobson/agents](https://github.com/wshobson/agents) 项目改进
- 感谢Python社区的所有贡献者
- 特别感谢Streamlit、CustomTkinter和Conda项目的维护者

---

**专注Python**: 简单高效，场景驱动 🐍