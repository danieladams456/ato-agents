# Local Development Setup Guide

This guide helps you set up a local development environment for the ATO Agents project without using the provided codespace/devcontainer.

## System Requirements

- **CPU**: 4+ cores recommended
- **Memory**: 16GB+ RAM recommended  
- **Storage**: 32GB+ free space recommended
- **Operating System**: Linux, macOS, or Windows with WSL2

## Prerequisites

### Required Software

1. **Python 3.8+**
   ```bash
   python3 --version
   ```

2. **Node.js LTS** (for any JavaScript tooling)
   - Install from [nodejs.org](https://nodejs.org/)
   - Or use a version manager like `nvm`

3. **Ollama**
   
## Setup Steps

### 1. Clone the Repository

```bash
git clone <repository-url>
cd ato-agents
```

### 2. Set Up Python Environment

Create and activate a Python virtual environment:

```bash
# Create virtual environment
python3 -m venv py_env

# Activate the environment
# On Linux/macOS:
source py_env/bin/activate

# On Windows:
# py_env\Scripts\activate
```

Add activation to your shell profile for convenience:
```bash
echo "source $(pwd)/py_env/bin/activate" >> ~/.bashrc
# or for zsh users:
# echo "source $(pwd)/py_env/bin/activate" >> ~/.zshrc
```

### 3. Install Python Dependencies

```bash
pip3 install -r requirements/requirements.txt
```

**Key Python packages installed:**
- **LangChain & Ollama integration**: `langchain`, `langchain-community`, `langchain-ollama`
- **Agent frameworks**: `langgraph`, `crewai`, `smolagents`, `autogen`  
- **RAG stack**: `chromadb`
- **Utilities**: `openai`, `pandas`, `sentence-transformers`, `pdfplumber`

### 4. Install and Configure Ollama

Ollama provides local LLM inference capabilities.

#### Install Ollama

**Linux/macOS:**
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

**Windows:**
- Download installer from [ollama.com](https://ollama.com/download)

#### Start Ollama Service

```bash
# Start Ollama server in background
ollama serve &
```

Wait for the service to be ready (usually 10-15 seconds).

#### Download Required Models

```bash
# Pull the llama3.2 model (this may take several minutes)
ollama pull llama3.2

# Verify installation
ollama list
```

### 5. Model Warmup (Recommended)

For faster first responses, warm up the model:

```bash
# Run warmup script if available
bash scripts/warmup.sh
```

This script will:
- Ensure the Python environment is properly activated
- Install additional warmup dependencies if needed
- Run initial model queries to cache responses

## Project Structure

- `agents/` - Main agent implementations
- `data/` - Sample datasets (CSV, PDF files)
- `requirements/` - Python dependency specifications
- `scripts/` - Setup and utility scripts
- `images/` - Documentation images
- `labs.md` - Learning labs and exercises

## Development Workflow

### Running Agents

Activate your Python environment first:
```bash
source py_env/bin/activate
```

Then run individual agents:
```bash
python agents/agent1.py
# or other agent files
```

### Working with Data

Sample data files are provided in the `data/` directory:
- `offices.csv` - Sample CSV data
- `offices.pdf` - Sample PDF document

### Testing Your Setup

1. **Verify Python environment:**
   ```bash
   python -c "import langchain, ollama; print('Dependencies OK')"
   ```

2. **Test Ollama connection:**
   ```bash
   ollama list
   ```

3. **Run a simple agent test:**
   ```bash
   python agents/goal.py
   ```

## Troubleshooting

### Common Issues

**Ollama not starting:**
- Ensure no other Ollama instances are running: `pkill ollama`
- Check system resources (16GB+ RAM recommended)
- Try starting with: `ollama serve --host 0.0.0.0`

**Python dependencies failing:**
- Ensure you're using Python 3.8+
- Update pip: `pip install --upgrade pip`
- Try installing dependencies one by one to isolate issues

**Model download issues:**
- Check internet connection
- Ensure sufficient disk space (models can be 4GB+)
- Try pulling specific model versions: `ollama pull llama3.2:latest`

**Environment activation:**
- Ensure virtual environment path is correct
- Re-run the environment setup steps
- Check shell profile modifications took effect

### Performance Optimization

- **Memory**: Close unnecessary applications, models require significant RAM
- **CPU**: Multi-core systems perform better for concurrent agent operations
- **Storage**: Use SSD storage for faster model loading

## Alternative Setup Methods

If the automated setup script doesn't work, you can run the manual setup:

```bash
bash scripts/setup.sh
```

This script handles the complete environment setup including:
- Python virtual environment creation
- Dependency installation  
- Ollama installation and configuration
- Model downloading and warmup

## VSCode Configuration (Optional)

For VSCode users, the project includes recommended settings:
- Python interpreter: `py_env/bin/python`
- Markdown files open in preview mode
- GitHub Copilot disabled (for learning purposes)

Install recommended extensions:
- `mathematic.vscode-pdf` - PDF viewing support

## Next Steps

Once your environment is set up:
1. Review `README.md` for project overview
2. Check out `labs.md` for hands-on exercises
3. Explore the `agents/` directory for example implementations
4. Run sample agents to verify everything works

## Getting Help

If you encounter issues:
1. Check the troubleshooting section above
2. Verify system requirements are met
3. Review error messages for specific dependency issues
4. Consider running the automated setup script instead
