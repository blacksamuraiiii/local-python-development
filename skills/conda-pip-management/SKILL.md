---
name: conda-pip-management
description: Master conda environments and pip package management for Python development workflows. Use when setting up Python projects, managing dependencies, creating virtual environments, or optimizing Python development with conda and pip.
---

# Conda Environment and Pip Package Management

Comprehensive guide to using conda environments combined with pip for Python package management, dependency resolution, and environment isolation.

## When to Use This Skill

- Setting up conda environments for Python development
- Managing project dependencies with conda + pip
- Creating isolated development environments
- Handling multiple Python versions with conda
- Managing conda channels and package sources
- Optimizing conda workflows for data science projects
- Migrating between conda environments and pip-only setups
- Managing complex dependency trees in conda environments

## Core Concepts

### 1. Conda Basics
- **Conda environments**: Isolated Python environments with managed dependencies
- **Conda channels**: Package repositories (defaults, conda-forge)
- **Environment files**: environment.yml specification files
- **Package management**: conda install vs pip install within environments
- **Python versioning**: Managing multiple Python versions
- **Cross-platform support**: Windows, macOS, Linux

### 2. Conda vs Pip Integration
- **Conda packages**: Binary packages with compiled extensions
- **pip packages**: Pure Python packages not available in conda
- **Mixed workflows**: Using both conda and pip in same environment
- **conda-forge**: Community-driven package channel
- **pip within conda**: Using pip inside conda environments

### 3. Environment Management
- **Environment creation**: Creating from environment.yml files
- **Environment cloning**: Copying existing environments
- **Environment updating**: Modifying existing environments
- **Environment removal**: Clean environment management
- **Environment activation**: Shell integration and activation
- **Environment export**: Portable environment specifications

## Quick Start

### Installation

```bash
# Install Miniconda (lightweight conda)
# macOS/Linux
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh

# Windows (PowerShell)
Invoke-WebRequest https://repo.anaconda.com/miniconda/Miniconda3-latest-Windows-x86_64.exe -OutFile Miniconda3-latest-Windows-x86_64.exe -UseBasicParsing
Start-Process Miniconda3-latest-Windows-x86_64.exe /S

# Or install full Anaconda (includes many packages)
# Use conda --help for more options
```

### Basic Commands

```bash
# Create new environment
conda create -n my-env python=3.12

# Create from environment.yml
conda env create -f environment.yml

# Activate environment
conda activate my-env

# Install packages
conda install numpy pandas matplotlib

# Install with conda-forge
conda install -c conda-forge scikit-learn

# Use pip within conda environment
pip install requests==2.31.0

# List environments
conda env list

# Remove environment
conda env remove -n my-env
```

## Environment Configuration

### environment.yml Structure

```yaml
# environment.yml
name: my-project
channels:
  - defaults
  - conda-forge
dependencies:
  - python=3.12
  - numpy>=1.24.0
  - pandas>=2.0.0
  - matplotlib>=3.7.0
  - pip:
    - requests>=2.31.0
    - fastapi>=0.104.0
    - pytest>=7.4.0
  - pip:
    - black>=23.0.0
    - ruff>=0.1.0
```

### Advanced environment.yml

```yaml
# environment.yml
name: data-science-env
channels:
  - defaults
  - conda-forge
  - pytorch
dependencies:
  - python=3.11
  - numpy
  - pandas
  - scikit-learn
  - jupyter
  - pip:
    - plotly>=5.15.0
    - dash>=2.14.0
    - streamlit>=1.28.0
variables:
  CUDA_VERSION: "11.8"
  PYTORCH_VERSION: "2.1.0"
prefix: C:\Users\username\miniconda3\envs\data-science-env
```

## Package Management Patterns

### Pattern 1: Pure Conda Workflow

```bash
# Create environment
conda create -n project-env python=3.12

# Activate environment
conda activate project-env

# Install conda packages
conda install numpy pandas scikit-learn jupyter matplotlib

# Install additional channels
conda install -c conda-forge fastapi uvicorn

# Update environment
conda env update -n project-env --file environment.yml

# Export environment
conda env export > environment.yml
```

### Pattern 2: Mixed Conda + Pip Workflow

```bash
# Create environment with pip requirements
conda create -n project-env python=3.12 pip

# Activate and install packages
conda activate project-env
conda install numpy pandas matplotlib
pip install requests==2.31.0 fastapi
pip install -r requirements.txt

# Install from specific index
pip install --index-url https://pypi.org/simple/ package-name

# Install development packages
conda install pip pytest black ruff mypy
pip install -e .[dev]

# Freeze requirements
conda env export > environment.yml
pip freeze > requirements-conda.txt
```

### Pattern 3: Multiple Environment Management

```bash
# List all environments
conda env list

# Create specific environment version
conda create -n project-env python=3.11 numpy=1.23.0

# Clone from existing environment
conda create --clone base-env -n new-env

# Remove environment
conda env remove -n old-env

# Clean up unused packages
conda clean --all
```

## Data Science Workflow

### Scientific Python Stack

```yaml
# environment.yml for data science
name: data-science
channels:
  - conda-forge
  - defaults
dependencies:
  - python=3.11
  - numpy>=1.24.0
  - pandas>=2.0.0
  - scipy>=1.10.0
  - matplotlib>=3.7.0
  - seaborn>=0.12.0
  - scikit-learn>=1.3.0
  - jupyter>=1.0.0
  - ipykernel>=6.25.0
  - pip:
    - plotly>=5.15.0
    - dash>=2.14.0
    - streamlit>=1.28.0
```

### Machine Learning Environment

```yaml
# environment.yml for ML
name: ml-environment
channels:
  - pytorch
  - conda-forge
dependencies:
  - python=3.11
  - pytorch
  - torchvision
  - torchaudio
  - pytorch-lightning>=2.0.0
  - pip:
    - transformers>=4.30.0
    - datasets>=2.12.0
    - accelerate>=0.20.0
    - wandb>=0.15.0
variables:
  PYTORCH_VERSION: "2.1.0"
```

## Development Workflows

### Pattern 4: Development Environment Setup

```bash
# Create development environment
conda create -n dev-env python=3.12 pip

# Activate environment
conda activate dev-env

# Install development tools
conda install pytest black ruff mypy
pip install pre-commit pytest-cov coverage

# Install linters and formatters
conda install flake8 isort
pip install autopep8 black[d] jupyter-black

# Install database connectors
conda install psycopg2 pymysql
pip install sqlalchemy alembic
```

### Pattern 5: Production Environment

```yaml
# environment.yml for production
name: prod-env
channels:
  - defaults
  - conda-forge
dependencies:
  - python=3.12
  - gunicorn>=21.2.0
  - uvicorn>=0.24.0
  - pip:
    - fastapi>=0.104.0
    - celery>=5.3.0
    - redis>=5.0.0
    - psycopg2-binary>=2.9.0
```

## Environment Variables

### Pattern 6: Environment Configuration

```bash
# Set environment variables
conda env config vars dev-env PYTHONPATH /custom/path
conda env config vars dev-env DATABASE_URL postgresql://user:pass@localhost/db

# List environment variables
conda env config vars dev-env

# Unset environment variables
conda env config vars dev-env --unset PYTHONPATH
conda env config vars dev-env --unset DATABASE_URL

# Use in scripts
echo $CONDA_DEFAULT_ENV
echo $CONDA_PREFIX
echo $PYTHONPATH
```

## Integration with Tools

### Pattern 7: IDE Integration

```bash
# VS Code integration
conda activate dev-env
code .  # Opens current directory in VS Code

# Jupyter integration
conda activate data-science
jupyter notebook
jupyter lab

# PyCharm integration
# Configure PyCharm to use conda interpreter
# Settings → Project → Python Interpreter → Add conda environment
```

### Pattern 8: Docker Integration

```dockerfile
# Dockerfile with conda
FROM continuumio/miniconda3

# Set working directory
WORKDIR /app

# Copy requirements
COPY requirements.txt .

# Create environment and install dependencies
RUN conda create -n app-env --file requirements.txt && \
    conda activate app-env && \
    pip install -e .

# Set environment variables
ENV CONDA_DEFAULT_ENV=app-env
ENV PATH=/opt/conda/envs/app-env/bin:$PATH

# Run application
CMD ["python", "app.py"]
```

## Best Practices

### Environment Management

1. **Use specific Python versions**: Pin Python version in environment.yml
2. **Separate dev and prod**: Different environments for development and production
3. **Use conda-forge**: Prefer conda-forge for newer package versions
4. **Document environments**: Keep environment.yml files in version control
5. **Regular cleanup**: Remove unused environments and packages
6. **Use pip within conda**: Install pure Python packages with pip inside conda

### Package Installation

1. **Prefer conda packages**: Use conda install for packages available in conda
2. **Specify versions**: Pin package versions for reproducibility
3. **Use pip when needed**: Install packages not available in conda
4. **Use channels**: Configure channels for package availability
5. **Avoid system packages**: Use conda packages instead of system packages

### Performance Optimization

1. **Use mamba**: Consider mamba for faster dependency resolution
2. **Parallel installs**: Enable parallel package installation
3. **Cache packages**: Enable conda package caching
4. **Clean environments**: Regularly clean package cache

### Collaboration

1. **Share environment.yml**: Commit environment files to version control
2. **Document setup**: Include environment setup in README
3. **Consistent channels**: Use consistent channels across team
4. **Version pinning**: Pin critical packages for consistency

## Command Reference

### Essential Commands

```bash
# Environment Management
conda create -n envname python=3.12          # Create environment
conda activate envname                         # Activate environment
conda deactivate                                # Deactivate environment
conda env remove -n envname                    # Remove environment
conda env list                                  # List environments
conda env export > environment.yml              # Export environment

# Package Management
conda install package-name                        # Install package
conda install -c conda-forge package-name         # Install from channel
conda update package-name                         # Update package
conda remove package-name                          # Remove package
conda list                                      # List installed packages
conda search package-name                          # Search packages
conda clean --all                               # Clean cache

# Pip within Conda
pip install package-name                            # Install pip package
pip install -r requirements.txt                   # Install from requirements
pip install --upgrade package-name                  # Upgrade package
pip uninstall package-name                          # Uninstall package
pip freeze > requirements.txt                       # Freeze requirements
pip list                                       # List pip packages

# Information
conda info                                       # Conda information
conda --version                                   # Conda version
python --version                                   # Python version in environment
which python                                     # Python location
```

### Troubleshooting

### Common Issues

**Environment activation issues**:
```bash
# Initialize conda for shell
conda init bash
conda init zsh
conda init fish

# Restart shell or run:
source ~/.bashrc
```

**Package conflicts**:
```bash
# Check package versions
conda list package-name

# Update specific package
conda update package-name

# Create clean environment
conda create -n clean-env --clone base-env python=3.12
```

**Path issues**:
```bash
# Check conda paths
conda info --base
conda info --envs

# Reset conda paths
conda config --set auto_activate_base false
```

## Automation

### Environment Scripts

```bash
#!/bin/bash
# setup-env.sh - Automated environment setup
ENV_NAME=$1
PYTHON_VERSION=${2:-3.12}

# Create environment if not exists
if ! conda env list | grep -q "^$ENV_NAME\s"; then
    echo "Creating conda environment: $ENV_NAME"
    conda create -n $ENV_NAME python=$PYTHON_VERSION pip
fi

# Activate environment
echo "Activating conda environment: $ENV_NAME"
conda activate $ENV_NAME

# Install basic development packages
echo "Installing development packages..."
conda install pytest black ruff mypy
pip install pre-commit pytest-cov

echo "Environment setup complete!"
```

### GitHub Actions Workflow

```yaml
# .github/workflows/conda-test.yml
name: Test with Conda

on: [push, pull_request]

jobs:
  test:
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest, macos-latest]
        python-version: [3.9, 3.10, 3.11]

    steps:
    - uses: actions/checkout@v3

    - name: Set up conda
      uses: conda-incubator/setup-miniconda@v2
      with:
        python-version: ${{ matrix.python-version }}
        activate-environment: test-env

    - name: Install dependencies
      run: |
        conda install numpy pandas pytest
        pip install requests

    - name: Run tests
      run: |
        pytest tests/ -v
```

## Resources

- **Official conda documentation**: https://docs.conda.io/en/latest/
- **conda cheat sheet**: https://docs.conda.io/projects/conda/en/latest/user-guide/cheatsheet.html
- **conda-forge**: https://conda-forge.org/
- **conda channel documentation**: https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-channels.html
- **pip documentation**: https://pip.pypa.io/en/stable/
- **Python packaging guide**: https://packaging.python.org/en/latest/