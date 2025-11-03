# CLAUDE.md - Python开发工作规则

## 🚀 核心约束
- 必须中文回复
- 任务优先调用适配的Python代理或技能
- 禁止恶意代码，通过安全检查

## 🐍 Python开发场景

### 主要用途与代理对应
```yaml
Python开发:
  - 通用Python开发: python-pro
  - 异步编程: python-pro + async-python-patterns
  - 性能优化: python-pro + python-performance-optimization
  - 测试开发: python-pro + python-testing-patterns

Web应用:
  - 数据仪表板: streamlit-pro
  - Web应用开发: streamlit-pro
  - 数据可视化: streamlit-pro

GUI桌面应用:
  - 界面开发: tkinter-pro
  - CustomTkinter应用: tkinter-pro
  - 桌面工具: tkinter-pro

应用打包:
  - PyInstaller打包: python-packaging
  - 可执行文件生成: python-packaging
  - 跨平台部署: python-packaging
```

### 🔧 技能系统
```yaml
核心技能:
  - async-python-patterns: asyncio高性能应用
  - python-testing-patterns: pytest, TDD, 测试策略
  - python-packaging: PyInstaller打包和部署
  - python-performance-optimization: 性能分析和优化
  - conda-pip-management: Conda环境+pip包管理
```

## 🎯 智能触发规则

### 使用场景触发
```yaml
通用Python开发:
  - .py文件: python-pro
  - "python": python-pro
  - "异步/async": python-pro + async-python-patterns
  - "性能优化": python-pro + python-performance-optimization

Web应用开发:
  - "streamlit": streamlit-pro
  - "dashboard/仪表板": streamlit-pro
  - "web应用": streamlit-pro
  - "数据可视化": streamlit-pro

GUI应用开发:
  - "tkinter": tkinter-pro
  - "gui/界面": tkinter-pro
  - "ctk": tkinter-pro
  - "desktop/桌面": tkinter-pro
  - "customtkinter": tkinter-pro

应用打包:
  - "打包": python-packaging
  - "pyinstaller": python-packaging
  - "exe/可执行文件": python-packaging
  - "部署": python-packaging
  - "跨平台": python-packaging

开发工具:
  - "测试": python-pro + python-testing-patterns
  - "tdd": python-pro + python-testing-patterns
  - "包管理": conda-pip-management
  - "conda": conda-pip-management
  - "pip": conda-pip-management
```

## 🛠️ MCP工具集成
```yaml
文档和知识:
  - context7: 获取最新Python技术文档

网络和自动化:
  - tavily-search: 智能网络搜索
  - mcp__fetch__fetch: 网络内容获取

开发工具:
  - mcp__ide__getDiagnostics: VS Code诊断
  - mcp__ide__executeCode: Jupyter代码执行
```

## ⚡ 开发原则
- **KISS**: 保持简单直接
- **TDD**: 测试驱动开发
- **Clean Code**: 编写可读、可维护的Python代码

## ✅ 质量检查清单
- [ ] 使用中文回复
- [ ] 已调用Python相关代理或技能
- [ ] 代码安全无害
- [ ] 遵循Python最佳实践
- [ ] 包含必要测试

## 🎯 工作流程
1. **分析场景**: 识别开发类型和需求
2. **选择代理**: 根据场景选择对应代理
3. **组合技能**: 根据需要调用相关技能
4. **质量验证**: 测试和代码审查

## 🔧 调用模式
```yaml
通用开发: Task工具调用python-pro
Web应用: Task工具调用streamlit-pro
GUI开发: Task工具调用tkinter-pro
应用打包: Skill工具调用python-packaging
特定技能: Skill工具直接调用对应技能
组合使用: Task工具+多个技能组合
```

---
**专注Python**: 简单高效，场景驱动 🐍