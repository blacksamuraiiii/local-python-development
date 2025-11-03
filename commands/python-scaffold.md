# Python Project Scaffolding (Local Conda + Pip Configuration)

您是Python项目架构专家，专门创建生产就绪的Python应用程序。使用conda环境管理和pip包管理，生成具有现代工具（Streamlit、PyInstaller）、类型提示、测试设置的完整项目结构，并遵循当前最佳实践。

## Context

用户需要自动化的Python项目脚手架，创建一致、类型安全的应用程序，具有适当的结构、依赖管理、测试和工具。专注于现代Python模式、Streamlit应用、GUI开发和可扩展架构。

## Requirements

$ARGUMENTS

## Instructions

### 1. 分析项目类型

根据用户需求确定项目类型：
- **Streamlit App**: 数据仪表板、Web应用、交互工具
- **CustomTkinter GUI**: 桌面应用程序、系统工具
- **Library**: 可重用包、实用工具、库
- **CLI**: 命令行工具、自动化脚本
- **Generic**: 标准Python应用程序

### 2. 使用Conda初始化项目

```bash
# 创建新的conda环境
conda create -n <project-name> python=3.12 -y
conda activate <project-name>

# 创建项目目录
mkdir <project-name>
cd <project-name>

# 初始化git仓库
git init
echo ".venv/" >> .gitignore
echo "*.pyc" >> .gitignore
echo "__pycache__/" >> .gitignore
echo ".pytest_cache/" >> .gitignore
echo ".ruff_cache/" >> .gitignore
echo "*.egg-info/" >> .gitignore
echo "dist/" >> .gitignore
echo "build/" >> .gitignore

# 创建基础结构
mkdir src
mkdir tests
mkdir docs
```

### 3. 生成Streamlit应用结构

```
streamlit-project/
├── environment.yml          # Conda环境配置
├── pyproject.toml          # 项目配置
├── README.md
├── .gitignore
├── .env.example
├── requirements.txt        # Pip依赖（可选）
├── src/
│   └── project_name/
│       ├── __init__.py
│       ├── main.py
│       ├── config.py
│       ├── pages/
│       │   ├── __init__.py
│       │   ├── dashboard.py
│       │   └── settings.py
│       ├── components/
│       │   ├── __init__.py
│       │   ├── charts.py
│       │   └── forms.py
│       ├── data/
│       │   ├── __init__.py
│       │   ├── loader.py
│       │   └── processor.py
│       └── utils/
│           ├── __init__.py
│           └── helpers.py
└── tests/
    ├── __init__.py
    ├── conftest.py
    └── test_app.py
```

**environment.yml**:
```yaml
name: project-name
channels:
  - conda-forge
  - defaults
dependencies:
  - python=3.12
  - numpy
  - pandas
  - matplotlib
  - seaborn
  - plotly
  - pip
  - pip:
    - streamlit>=1.28.0
    - pydantic>=2.5.0
    - python-dotenv>=1.0.0
    - altair>=5.2.0
    - pytest>=7.4.0
    - ruff>=0.1.0
```

**pyproject.toml**:
```toml
[project]
name = "project-name"
version = "0.1.0"
description = "Streamlit data application"
requires-python = ">=3.11"
dependencies = [
    "streamlit>=1.28.0",
    "pydantic>=2.5.0",
    "python-dotenv>=1.0.0",
    "altair>=5.2.0",
    "numpy>=1.24.0",
    "pandas>=2.0.0",
    "matplotlib>=3.7.0",
    "seaborn>=0.12.0",
]

[project.optional-dependencies]
dev = [
    "pytest>=7.4.0",
    "pytest-cov>=4.1.0",
    "ruff>=0.1.0",
    "mypy>=1.7.0",
]

[tool.ruff]
line-length = 100
target-version = "py311"

[tool.ruff.lint]
select = ["E", "F", "I", "N", "W", "UP"]

[tool.pytest.ini_options]
testpaths = ["tests"]
```

**src/project_name/main.py**:
```python
import streamlit as st
from pathlib import Path
import sys

# 添加src到路径
sys.path.append(str(Path(__file__).parent.parent))

from .config import settings
from .pages import dashboard, settings_page
from .components import charts

def main():
    st.set_page_config(
        page_title=settings.APP_NAME,
        page_icon="📊",
        layout="wide",
        initial_sidebar_state="expanded"
    )

    st.title(f"📊 {settings.APP_NAME}")
    st.markdown(f"**{settings.APP_DESCRIPTION}**")

    # 侧边栏导航
    page = st.sidebar.selectbox("选择页面", [
        "Dashboard", "Settings", "Data Analysis"
    ])

    if page == "Dashboard":
        dashboard.show()
    elif page == "Settings":
        settings_page.show()
    elif page == "Data Analysis":
        charts.show_analysis()

if __name__ == "__main__":
    main()
```

### 4. 生成CustomTkinter GUI应用结构

```
tkinter-project/
├── environment.yml
├── pyproject.toml
├── build.py              # PyInstaller构建脚本
├── build.spec            # PyInstaller规范文件
├── README.md
├── .gitignore
├── src/
│   └── project_name/
│       ├── __init__.py
│       ├── main.py
│       ├── config.py
│       ├── views/
│       │   ├── __init__.py
│       │   ├── main_window.py
│       │   ├── settings_dialog.py
│       │   └── about_dialog.py
│       ├── components/
│       │   ├── __init__.py
│       │   ├── custom_widgets.py
│       │   └── status_bar.py
│       ├── models/
│       │   ├── __init__.py
│       │   └── app_data.py
│       └── utils/
│           ├── __init__.py
│           ├── config_manager.py
│           └── file_handler.py
├── assets/
│   ├── icons/
│   └── images/
└── tests/
    ├── __init__.py
    └── test_gui.py
```

**environment.yml**:
```yaml
name: tkinter-project
channels:
  - conda-forge
  - defaults
dependencies:
  - python=3.12
  - pip
  - pip:
    - customtkinter>=5.2.0
    - pillow>=10.0.0
    - pydantic>=2.5.0
    - pyinstaller>=6.0.0
    - auto-py-to-exe>=2.20.0
```

**build.spec** (PyInstaller):
```python
# -*- mode: python ; coding: utf-8 -*-

block_cipher = None

a = Analysis(
    ['src/project_name/main.py'],
    pathex=['src'],
    binaries=[],
    datas=[
        ('assets', 'assets'),
    ],
    hiddenimports=[
        'PIL._tkinter_finder',
        'customtkinter',
    ],
    hookspath=[],
    hooksconfig={},
    runtime_hooks=[],
    excludes=[],
    win_no_prefer_redirects=False,
    win_private_assemblies=False,
    cipher=block_cipher,
    noarchive=False,
)

pyz = PYZ(a.pure, a.zipped_data, cipher=block_cipher)

exe = EXE(
    pyz,
    a.scripts,
    a.binaries,
    a.zipfiles,
    a.datas,
    [],
    name='app_name',
    debug=False,
    bootloader_ignore_signals=False,
    strip=False,
    upx=True,
    upx_exclude=[],
    runtime_tmpdir=None,
    console=False,
    disable_windowed_traceback=False,
    argv_emulation=False,
    target_arch=None,
    codesign_identity=None,
    entitlements_file=None,
    icon='assets/icons/app_icon.ico'
)
```

**build.py**:
```python
#!/usr/bin/env python3
"""PyInstaller构建脚本"""

import os
import sys
import subprocess
from pathlib import Path

def build_executable():
    """构建可执行文件"""

    # 检查环境
    if not os.path.exists("src/project_name/main.py"):
        print("错误: 找不到main.py文件")
        return False

    # 清理旧的构建
    for path in ["build", "dist", "*.spec"]:
        if os.path.exists(path):
            subprocess.run(["rm", "-rf", path], shell=True)

    # 运行PyInstaller
    cmd = [
        "pyinstaller",
        "--onefile",
        "--windowed",
        "--add-data=assets:assets",
        "--icon=assets/icons/app_icon.ico",
        "--name=app_name",
        "src/project_name/main.py"
    ]

    print("构建可执行文件...")
    result = subprocess.run(cmd, capture_output=True, text=True)

    if result.returncode == 0:
        print("✅ 构建成功!")
        print(f"可执行文件位于: {Path('dist/app_name.exe').absolute()}")
        return True
    else:
        print("❌ 构建失败:")
        print(result.stderr)
        return False

if __name__ == "__main__":
    success = build_executable()
    sys.exit(0 if success else 1)
```

### 5. 生成Python库结构

```
library-name/
├── environment.yml
├── pyproject.toml
├── README.md
├── LICENSE
├── src/
│   └── library_name/
│       ├── __init__.py
│       ├── py.typed
│       ├── core.py
│       └── utils.py
└── tests/
    ├── __init__.py
    ├── test_core.py
    └── test_utils.py
```

**pyproject.toml for Library**:
```toml
[build-system]
requires = ["setuptools>=61.0", "wheel"]
build-backend = "setuptools.build_meta"

[project]
name = "library-name"
version = "0.1.0"
description = "Library description"
readme = "README.md"
requires-python = ">=3.11"
license = {text = "MIT"}
authors = [
    {name = "Your Name", email = "email@example.com"}
]
classifiers = [
    "Programming Language :: Python :: 3",
    "License :: OSI Approved :: MIT License",
]

[project.optional-dependencies]
dev = [
    "pytest>=7.4.0",
    "pytest-cov>=4.1.0",
    "ruff>=0.1.0",
    "mypy>=1.7.0",
    "setuptools>=61.0",
    "wheel",
]

[tool.setuptools.packages.find]
where = ["src"]

[tool.setuptools.package-data]
library_name = ["py.typed"]
```

### 6. 生成CLI工具结构

```python
# pyproject.toml
[project.scripts]
cli-name = "project_name.cli:main"

[project]
dependencies = [
    "typer>=0.9.0",
    "rich>=13.7.0",
    "click>=8.1.0",
]
```

**src/project_name/cli.py**:
```python
import typer
from rich.console import Console
from rich.table import Table

app = typer.Typer()
console = Console()

@app.command()
def hello(name: str = typer.Option(..., "--name", "-n", help="您的名字")):
    """问候某人"""
    console.print(f"[bold green]你好 {name}![/bold green]")

@app.command()
def version():
    """显示版本信息"""
    console.print("[bold blue]版本 1.0.0[/bold blue]")

def main():
    app()
```

### 7. 配置开发工具

**.env.example**:
```env
# 应用程序配置
APP_NAME="My Application"
VERSION="0.1.0"
DEBUG=True

# 数据库配置
DATABASE_URL="sqlite:///./app.db"

# API配置
API_KEY="your-api-key-here"
API_BASE_URL="https://api.example.com"

# 文件路径
DATA_DIR="./data"
LOG_DIR="./logs"
```

**Makefile**:
```makefile
.PHONY: install dev test lint format clean build

install:
	conda env create -f environment.yml
	conda activate project-name

dev:
	streamlit run src/project_name/main.py

test:
	python -m pytest tests/ -v

lint:
	ruff check .
	ruff format --check .

format:
	ruff format .

clean:
	find . -type d -name __pycache__ -exec rm -rf {} +
	find . -type f -name "*.pyc" -delete
	rm -rf .pytest_cache .ruff_cache build dist *.egg-info

build:
	python build.py

install-dev:
	pip install -e .
```

## 输出格式

1. **项目结构**: 包含所有必要文件的完整目录树
2. **配置**: 使用conda和pip的environment.yml和pyproject.toml
3. **入口点**: 主应用程序文件（main.py、cli.py等）
4. **测试**: 使用pytest配置的测试结构
5. **文档**: 包含设置和使用说明的README
6. **开发工具**: Makefile、.env.example、.gitignore、build.py
7. **构建配置**: PyInstaller的build.spec和构建脚本

专注于创建具有现代工具、类型安全、全面测试设置和GUI应用支持的生产就绪Python项目。