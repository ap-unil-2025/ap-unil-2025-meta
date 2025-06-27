---
layout: assignment
title: "Assignment 2: Python Fundamentals & Testing"
assignment_number: 2
due_date: 2025-03-01 23:59:00
points: 120
difficulty: "Intermediate"
estimated_time: "5-6 hours"
github_classroom_url: "https://classroom.github.com/a/placeholder-assignment-2"
starter_repo: "ap2025-assignment-2-python"
topics:
  - "Python programming"
  - "Unit testing"
  - "Code documentation"
  - "Error handling"
status: "open"
---

## Overview

Build a command-line tool in Python that demonstrates fundamental programming concepts, testing practices, and proper documentation. This assignment emphasizes clean code, test-driven development, and professional software practices.

## Learning Objectives

- Write clean, maintainable Python code
- Implement comprehensive unit tests
- Handle errors gracefully
- Document code effectively
- Use virtual environments and dependency management

## Getting Started

1. **Accept the assignment** via GitHub Classroom link
2. **Set up your environment**:
   ```bash
   python -m venv venv
   source venv/bin/activate  # or `venv\Scripts\activate` on Windows
   pip install -r requirements.txt
   ```
3. **Run the test suite** to understand the requirements:
   ```bash
   pytest tests/
   ```

## Project Requirements

### Core Functionality (60 points)
Build a **File Analyzer** tool that:
- Analyzes text files for various statistics
- Supports multiple file formats (.txt, .md, .py)
- Provides word count, line count, character analysis
- Identifies common patterns and keywords

### Testing Suite (30 points)
- Minimum 90% test coverage
- Unit tests for all core functions
- Integration tests for file processing
- Edge case handling (empty files, large files, invalid formats)

### Documentation (20 points)
- Comprehensive README with usage examples
- Docstrings for all functions and classes
- Type hints throughout the codebase
- Contributing guidelines

### Code Quality (10 points)
- Follows PEP 8 style guidelines
- No code smells or anti-patterns
- Proper error handling and logging
- Efficient algorithms and data structures

## Technical Requirements

- **Python 3.9+** required
- **Dependencies**: Use `requirements.txt` for all packages
- **Testing**: pytest framework
- **Formatting**: Black code formatter
- **Linting**: flake8 or pylint
- **Type Checking**: mypy (optional but recommended)

## Deliverables

Your repository should include:

```
assignment-2/
├── src/
│   ├── __init__.py
│   ├── analyzer.py
│   ├── file_parser.py
│   └── utils.py
├── tests/
│   ├── __init__.py
│   ├── test_analyzer.py
│   ├── test_file_parser.py
│   └── test_integration.py
├── docs/
│   └── API.md
├── requirements.txt
├── setup.py
└── README.md
```

## Submission

- All code committed and pushed to your GitHub repository
- Include a `REFLECTION.md` file discussing:
  - Challenges encountered
  - Design decisions made
  - What you learned
  - Areas for improvement

## Bonus Opportunities (+10 points each)

- **Performance Analysis**: Benchmark your tool with large files
- **CLI Interface**: Add argument parsing with `argparse` or `click`
- **Configuration**: Support config files (YAML/JSON)
- **Parallel Processing**: Multi-threaded file processing

## Common Pitfalls to Avoid

- ❌ Not handling file encoding issues
- ❌ Missing edge cases in tests
- ❌ Poor error messages for users
- ❌ Hardcoded file paths or configurations
- ❌ Not validating input parameters

---

*Due: {{ page.due_date | date: "%B %d, %Y at %I:%M %p" }} • Points: {{ page.points }} • Difficulty: {{ page.difficulty }}*