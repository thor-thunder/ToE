---
name: readme-skill-import
description: Import and integrate readme-ai functionality for automated README generation
---

# ReadmeAI Skill Import

## Overview

This skill helps integrate the **readme-ai** tool into your Claude Code workflow for automated README file generation across repositories.

## What is readme-ai?

`readme-ai` is a Python-based tool that automatically generates comprehensive README files for any code repository. It:

- **Automates** detailed README creation with a single command
- **Supports** multiple LLM providers (OpenAI, Anthropic, Google Gemini, Ollama, offline mode)
- **Customizes** headers, badges, styles, and layouts
- **Analyzes** code structure to generate contextual documentation
- **Works** with any programming language or framework

## Quick Start

### Prerequisites

- Python 3.9 or higher
- pip, pipx, or uv package manager
- (Optional) API key for LLM provider (OpenAI, Anthropic, Gemini, etc.)

### Installation

```bash
# Using pip (recommended)
pip install -U readmeai

# Using pipx (isolated environment)
pipx install readmeai

# Using uv (fastest)
uv tool install readmeai
```

### Basic Usage

Generate a README for a repository:

```bash
# From a GitHub URL
readmeai --api openai --repository https://github.com/user/repo

# From a local directory
readmeai --api openai --repository /path/to/local/repo

# With custom styling
readmeai --api openai \
         --repository https://github.com/user/repo \
         --header-style modern \
         --badge-style flat-square \
         --output readme.md
```

## Configuration Options

| Option | Description | Default |
|--------|-------------|---------|
| `--api` | LLM provider (openai, anthropic, gemini, ollama, offline) | `offline` |
| `--model` | Specific LLM model to use | `gpt-3.5-turbo` |
| `--repository` | Repository URL or local path | Required |
| `--output` | Output README filename | `readme-ai.md` |
| `--header-style` | Header template style | `classic` |
| `--badge-style` | Badge icon style | `flat` |
| `--logo` | Project logo type | `blue` |
| `--temperature` | Creativity level (0.0-1.0) | `0.1` |
| `--tree-max-depth` | Directory tree depth | `2` |

## LLM Provider Setup

### OpenAI

```bash
export OPENAI_API_KEY=your_api_key
readmeai --api openai --repository https://github.com/user/repo
```

### Anthropic (Claude)

```bash
export ANTHROPIC_API_KEY=your_api_key
readmeai --api anthropic --model claude-3-5-sonnet-20240620 --repository https://github.com/user/repo
```

### Google Gemini

```bash
export GOOGLE_API_KEY=your_api_key
readmeai --api gemini --model gemini-1.5-flash --repository https://github.com/user/repo
```

### Ollama (Local)

```bash
# Start Ollama server
ollama pull llama3.2
ollama serve

# In another terminal
readmeai --api ollama --model llama3.2 --repository https://github.com/user/repo
```

### Offline Mode

```bash
readmeai --api offline --repository https://github.com/user/repo
```

## Advanced Usage

### Customizing README Styling

Create a modern, compact README with custom colors:

```bash
readmeai --api openai \
         --repository https://github.com/user/repo \
         --header-style modern \
         --badge-color FF4B4B \
         --badge-style flat-square \
         --navigation-style fold \
         --logo custom \
         --align left
```

### Docker Usage

```bash
docker pull zeroxeli/readme-ai:latest

docker run -it --rm \
  -e OPENAI_API_KEY=$OPENAI_API_KEY \
  -v "$(pwd)":/app zeroxeli/readme-ai:latest \
  --repository https://github.com/user/repo \
  --api openai
```

### Filtering with .readmeaiignore

Create a `.readmeaiignore` file in your repo to exclude files and directories:

```
# Ignore node_modules and build artifacts
node_modules/
dist/
build/
*.pyc
.venv/
__pycache__/

# Ignore test files
test/
tests/
```

## Generated README Sections

ReadmeAI automatically generates:

1. **Project Introduction** - Captured essence and value proposition
2. **Features Table** - Detailed feature breakdown
3. **Project Structure** - Visual directory tree
4. **Project Index** - Key modules and overview
5. **Getting Started** - Installation and dependencies
6. **Usage Guides** - Setup and usage instructions
7. **Testing** - Test command examples
8. **Contributing** - Contribution guidelines
9. **License** - License information
10. **Community** - Development roadmap and support

## Troubleshooting

### API Key Issues

Ensure your API key environment variable is set:

```bash
# Verify OpenAI key
echo $OPENAI_API_KEY

# Verify Anthropic key
echo $ANTHROPIC_API_KEY
```

### Permission Errors

For local repositories, ensure proper read permissions:

```bash
chmod -R 755 /path/to/repo
```

### Network/Proxy Issues

If behind a proxy, configure your environment:

```bash
export HTTP_PROXY=http://proxy.example.com:8080
export HTTPS_PROXY=http://proxy.example.com:8080
```

## Resources

- **GitHub Repository:** https://github.com/eli64s/readme-ai
- **Documentation:** https://eli64s.github.io/readme-ai
- **PyPI Package:** https://pypi.org/project/readmeai/
- **Issues & Discussions:** https://github.com/eli64s/readme-ai/issues

## Integration Examples

### Generate README for Current Project

```bash
readmeai --api anthropic \
         --repository . \
         --output README_GENERATED.md
```

### Batch Process Multiple Repos

```bash
for repo in repo1 repo2 repo3; do
  readmeai --api openai \
           --repository https://github.com/user/$repo \
           --output ${repo}-README.md
done
```

### Use in CI/CD Pipeline

Create a GitHub Actions workflow to auto-generate READMEs:

```yaml
name: Generate README
on: [push]
jobs:
  generate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Install readmeai
        run: pip install readmeai
      - name: Generate README
        env:
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
        run: readmeai --api openai --repository . --output README.md
      - name: Commit changes
        run: |
          git config --local user.email "action@github.com"
          git config --local user.name "GitHub Action"
          git add README.md
          git commit -m "docs: auto-generate README" || true
          git push
```

## Tips & Best Practices

1. **Start Offline:** Use `--api offline` for quick previews
2. **Test Styles:** Experiment with different `--header-style` and `--badge-style` options
3. **Custom Logos:** Use `--logo custom` to provide your own logo
4. **Iterate:** Generate multiple versions and choose the best one
5. **Review & Edit:** Always review generated content before committing

## Help & Support

Run `readmeai --help` to see all available options and latest updates.

For issues or feature requests, visit the [GitHub Issues](https://github.com/eli64s/readme-ai/issues) page.
