---
name: python-packaging
description: Create distributable Python applications using PyInstaller for standalone executables. Use when creating desktop apps, GUI tools, or distributing Python code to non-developers.
---

# Python Application Packaging with PyInstaller

Comprehensive guide to creating standalone Python executables using PyInstaller for easy distribution without requiring Python installation.

## When to Use This Skill

- Creating standalone desktop applications
- Building GUI applications (tkinter, CustomTkinter, etc.)
- Distributing Python tools to non-technical users
- Creating portable executables for Windows/macOS/Linux
- Packaging applications with dependencies
- Creating installers for end users
- Building one-file executables
- Distributing applications without Python environment requirements

## Core Concepts

### 1. PyInstaller Basics
- **Standalone executables**: No Python installation required
- **Bundled dependencies**: All libraries included in executable
- **Cross-platform support**: Windows, macOS, Linux
- **One-file option**: Single executable distribution
- **Folder distribution**: Executable with supporting files

### 2. PyInstaller Modes
- **One-file mode**: `--onefile` - single executable
- **One-directory mode**: `--onedir` - executable in folder
- **Windowed mode**: `--windowed` - no console window
- **Console mode**: `--console` - with console access

### 3. Build System
- **PyInstaller**: Converts Python to native executables
- **Spec files**: Python build configuration scripts
- **Hooks**: Custom build steps and post-processing
- **Analysis phase**: Scans for imports and dependencies

### 4. Distribution Targets
- **Windows**: .exe with optional installer
- **macOS**: .app bundle for macOS applications
- **Linux**: Standalone executable for Linux distributions

## Quick Start

### Installation

```bash
# Install PyInstaller
pip install pyinstaller

# Or with uv (recommended)
uv add pyinstaller
```

### Basic Commands

```bash
# Build one-file executable
pyinstaller --onefile main.py

# Build one-directory executable
pyinstaller --onedir main.py

# Build with windowed mode (no console)
pyinstaller --windowed main.py

# Build with custom icon
pyinstaller --icon=assets/icons/app.ico main.py

# Build with name and version
pyinstaller --name="MyApp" --version="1.0.0" main.py

# Build with additional data files
pyinstaller --add-data="assets/data:assets" main.py
```

## Application Structure

### Recommended Structure

```
my-app/
├── main.py                 # Main application entry point
├── requirements.txt          # Dependencies
├── README.md              # Application documentation
├── assets/
│   ├── icons/
│   │   ├── app.ico      # Windows icon
│   │   ├── app.icns     # macOS icon
│   │   └── app.png      # Linux icon
│   └── data/
│       └── config.json
├── build/
│   └── my_app.spec       # PyInstaller spec file
└── dist/
    ├── my_app.exe        # Windows executable
    ├── my_app.app        # macOS app bundle
    └── my_app           # Linux executable
```

### Simple main.py Example

```python
import tkinter as tk
from tkinter import ttk
import json
import os

class App:
    def __init__(self):
        self.root = tk.Tk()
        self.root.title("My Application")
        self.root.geometry("800x600")

        # Load data files
        self.config = self.load_config()

        # Create UI
        self.create_widgets()

    def load_config(self):
        """Load configuration from bundled data files."""
        try:
            # PyInstaller sets this path for bundled data
            base_path = getattr(sys, '_MEIPASS', os.path.dirname(os.path.abspath(__file__)))
            config_path = os.path.join(base_path, 'assets', 'data', 'config.json')

            with open(config_path, 'r') as f:
                return json.load(f)
        except Exception as e:
            print(f"Config loading error: {e}")
            return {}

    def create_widgets(self):
        """Create application widgets."""
        # Main frame
        main_frame = ttk.Frame(self.root, padding="10")
        main_frame.grid(row=0, column=0, sticky=(tk.W, tk.E, tk.N, tk.S))

        # Example widgets
        ttk.Label(main_frame, text="Hello World!").grid(row=0, column=0, pady=5)
        ttk.Button(main_frame, text="Click Me", command=self.on_click).grid(row=1, column=0, pady=5)

    def on_click(self):
        """Handle button click."""
        print("Button clicked!")

    def run(self):
        """Start the application."""
        self.root.mainloop()

if __name__ == "__main__":
    app = App()
    app.run()
```

## Advanced Configuration

### Custom Spec Files

```python
# build/my_app.spec
# -*- mode: python ; coding: utf-8 -*-

block_cipher = None

a = Analysis(['main.py'],
             pathex=['.'],
             binaries=[],
             datas=[('assets/data', 'assets/data')],  # Bundle data files
             hiddenimports=[],
             hookspath=['hooks'],
             runtime_hooks=[],
             excludes=[],
             win_no_prefer_redirects=False,
             win_private_assemblies=False,
             cipher=None,
             noarchive=False)

pyz = PYZ(a.pure, a.zipped_data,
             cipher=block_cipher)

exe = EXE(pyz,
          a.scripts,
          a.binaries,
          a.zipfiles,
          name='MyApp',
          debug=False,
          bootloader_ignore_signals=False,
          strip=False,
          upx=True,
          upx_exclude=[],
          runtime_tmpdir=None,
          console=True,  # Set to False for GUI apps
          disable_windowed_traceback=False,
          argv_emulation=False,
          target_arch=None,
          codesign_identity=None,
          entitlements_file=None,
          icon='assets/icons/app.ico')

coll = COLLECT(exe,
               a.binaries,
               a.zipfiles,
               strip=False,
               upx=True,
               upx_exclude=[],
               name='MyApp')
```

### Building with Spec File

```bash
# Build using custom spec
pyinstaller build/my_app.spec

# Clean build
pyinstaller --clean build/my_app.spec

# Build with log
pyinstaller --log-level DEBUG build/my_app.spec
```

## Platform-Specific Patterns

### Windows Applications

```bash
# Windows executable with icon
pyinstaller --onefile --windowed --icon=assets/icons/app.ico --name="MyApp" main.py

# Create Windows installer (using Inno Setup after PyInstaller)
# First build the app, then use installer tools
```

### macOS Applications

```bash
# macOS app bundle with icon
pyinstaller --windowed --icon=assets/icons/app.icns --name="MyApp" --osx-bundle-identifier=com.company.myapp main.py

# Create DMG installer (using create-dmg after PyInstaller)
# First build the app, then use create-dmg tool
```

### Linux Applications

```bash
# Linux executable
pyinstaller --onefile --name="my-app" main.py

# Create AppImage (using appimagetool after PyInstaller)
# First build the app, then create AppImage
```

## Dependencies Management

### requirements.txt for PyInstaller

```txt
# Core dependencies
tkinter  # Usually built-in, but specify if needed
customtkinter>=5.0.0
requests>=2.28.0
pillow>=9.0.0
numpy>=1.24.0

# PyInstaller specific dependencies
pyinstaller>=5.0.0
```

### Handling Hidden Imports

```python
# In spec file, for packages that PyInstaller can't detect
a = Analysis(['main.py'],
             hiddenimports=['tkinter', 'customtkinter'],
             # ... other options
            )
```

## Best Practices

### 1. Application Structure
- Keep main.py as the entry point
- Separate GUI logic into modules
- Use relative paths for bundled assets
- Handle both bundled and development environments

### 2. Cross-Platform Considerations
- Test on all target platforms
- Use appropriate file formats for icons (.ico, .icns, .png)
- Consider platform-specific packaging (installers, bundles)

### 3. Performance Optimization
- Use `--exclude-module` to remove unused dependencies
- Enable UPX compression for smaller executables
- Consider one-directory vs one-file trade-offs

### 4. Error Handling
- Handle missing bundled data files gracefully
- Provide fallback configurations
- Log errors to help users troubleshoot

## Troubleshooting

### Common Issues

**Module not found**:
```bash
# Add hidden imports in spec file
pyinstaller --hidden-import=module_name main.py
```

**Missing data files**:
```python
# Use correct path handling in code
import sys
import os

if getattr(sys, 'frozen', False):
    # Running as PyInstaller executable
    base_path = sys._MEIPASS
else:
    # Running in development
    base_path = os.path.dirname(__file__)

data_path = os.path.join(base_path, 'assets', 'data')
```

**Antivirus false positives**:
- Code-sign executables on Windows
- Use reputable download sources
- Consider Microsoft Defender SmartScreen

### Debug Options

```bash
# Verbose build output
pyinstaller --log-level DEBUG main.py

# Don't delete temporary files
pyinstaller --debug main.py

# Generate console output for GUI apps
pyinstaller --debug-all --windowed main.py
```

## Automation

### Build Script

```python
# build.py
import subprocess
import sys
import os

def build_executable():
    """Build the executable using PyInstaller."""
    print("Building executable...")

    # PyInstaller command
    cmd = [
        'pyinstaller',
        '--onefile',
        '--windowed',
        '--name=MyApp',
        '--icon=assets/icons/app.ico',
        '--add-data=assets/data:assets',
        '--clean',
        'main.py'
    ]

    try:
        result = subprocess.run(cmd, check=True, capture_output=True, text=True)
        print("Build successful!")
        print(result.stdout)
    except subprocess.CalledProcessError as e:
        print(f"Build failed: {e}")
        print(f"Error output: {e.stderr}")
        return False

    return True

if __name__ == "__main__":
    success = build_executable()
    sys.exit(0 if success else 1)
```

### GitHub Actions Build

```yaml
# .github/workflows/build.yml
name: Build Executable

on:
  push:
    tags: ['v*']
  pull_request:

jobs:
  build:
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest, macos-latest]

    steps:
    - uses: actions/checkout@v3

    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.11'

    - name: Install dependencies
      run: |
        pip install pyinstaller customtkinter requests

    - name: Build executable
      run: |
        pyinstaller --onefile --windowed --name="MyApp" main.py

    - name: Upload artifacts
      uses: actions/upload-artifact@v3
      with:
        name: ${{ matrix.os }}-executable
        path: dist/
```

## Distribution

### Creating Installers

**Windows**:
```bash
# Use Inno Setup for Windows installer
pip install innosetup
# Create .iss script and compile
```

**macOS**:
```bash
# Use create-dmg for macOS installer
pip install create-dmg
create-dmg "dist/MyApp.app" "MyApp-1.0.0.dmg"
```

**Linux**:
```bash
# Use AppImageTool for Linux portable app
# Install AppImageTool and create AppImage
```

## Resources

- **PyInstaller Documentation**: https://pyinstaller.readthedocs.io/
- **PyInstaller GitHub**: https://github.com/pyinstaller/pyinstaller
- **CustomTkinter**: https://customtkinter.tomschumann.dev/
- **Application Packaging**: Best practices for desktop applications