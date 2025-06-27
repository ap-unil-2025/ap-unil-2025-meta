---
layout: lesson
title: "Code Like a Scientist: Essential Tools"
week: 1
date: 2025-01-27
type: "hands-on"
topics:
  - Command line basics
  - Git version control
  - Python environment setup
  - Research programming workflow
slides: "/slides/practice/week01_slides.html"
code_examples: 
  - git-basics.py
  - environment-setup.sh
summary: "Hands-on tutorial covering essential programming tools for researchers including Git, command line, and Python environment setup."
---

# Code Like a Scientist: Essential Tools for Research Programming

This lesson introduces the fundamental tools every research programmer needs to work effectively and reproducibly.

## Learning Objectives

By the end of this lesson, you will:

- Navigate the command line confidently
- Use Git for version control of your research code
- Set up a professional Python development environment
- Understand research programming best practices
- Create reproducible research workflows

## Essential Tools Overview

### 1. Command Line Interface (CLI)
The command line is your gateway to powerful programming tools and efficient file management.

**Key Commands:**
```bash
# Navigation
ls          # List files
cd          # Change directory
pwd         # Print working directory

# File operations
mkdir       # Create directory
cp          # Copy files
mv          # Move/rename files
rm          # Remove files
```

### 2. Git Version Control
Git tracks changes in your code and enables collaboration.

**Basic Workflow:**
```bash
# Initialize repository
git init

# Track changes
git add .
git commit -m "Descriptive message"

# Sync with remote
git push origin main
git pull origin main
```

### 3. Python Environment Management
Professional Python development requires proper environment management.

**Using UV (recommended):**
```bash
# Create virtual environment
uv venv .venv

# Activate environment
source .venv/bin/activate  # macOS/Linux
# or
.venv\Scripts\activate     # Windows

# Install packages
uv pip install package-name
```

## Hands-on Activities

### Activity 1: Command Line Navigation
1. Open your terminal
2. Navigate to your Documents folder
3. Create a new directory called `research-projects`
4. List the contents to verify creation

### Activity 2: First Git Repository
1. Initialize a Git repository in your project folder
2. Create a simple Python file
3. Add and commit your changes
4. Check the commit history

### Activity 3: Python Environment Setup
1. Create a virtual environment for your project
2. Install commonly used research packages
3. Create a requirements.txt file
4. Test your environment

## Research Programming Workflow

1. **Project Setup**: Create organized directory structure
2. **Version Control**: Initialize Git repository
3. **Environment**: Set up isolated Python environment
4. **Development**: Write code with proper documentation
5. **Testing**: Validate your code works correctly
6. **Sharing**: Push to GitHub for collaboration

## Code Examples

See the accompanying code examples for practical implementations:
- `git-basics.py`: Common Git operations in Python
- `environment-setup.sh`: Automated environment setup script

## Resources

- **Slides**: [Session 1 Slides]({{ page.slides }})
- **Git Documentation**: [git-scm.com](https://git-scm.com/doc)
- **UV Documentation**: [astral.sh/uv](https://docs.astral.sh/uv/)
- **Command Line Cheat Sheet**: Available in course materials

## Troubleshooting

**Common Issues:**
- Git permission errors: Check SSH key setup
- Python environment conflicts: Use virtual environments
- Command not found: Verify software installation

## Assessment

This lesson contributes to:
- Assignment 1: Git Basics
- Final project setup and version control

## Next Steps

Continue with the next lesson to build on these foundational tools.