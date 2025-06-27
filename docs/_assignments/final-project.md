---
layout: assignment
title: "Final Project: Research Software Development"
assignment_number: "Final"
due_date: 2025-04-20 23:59:00
points: 300
difficulty: "Advanced"
estimated_time: "15-20 hours"
github_classroom_url: "https://classroom.github.com/a/placeholder-final-project"
starter_repo: "ap2025-final-project-template"
topics:
  - "Software architecture"
  - "Research reproducibility"
  - "Data analysis"
  - "Documentation"
  - "Deployment"
status: "coming_soon"
team_size: "1-3 students"
---

## Overview

Design and implement a complete research software project that demonstrates advanced programming concepts, software engineering best practices, and reproducible research principles. This capstone project integrates all course concepts into a real-world application.

## Project Goals

Create a research-oriented software tool that:
- Solves a genuine research problem
- Demonstrates technical proficiency
- Follows industry best practices
- Is fully documented and reproducible
- Can be used by other researchers

## Learning Objectives

- Apply software architecture principles
- Implement comprehensive testing strategies
- Create reproducible research pipelines
- Practice code review and collaboration
- Deploy and maintain research software

## Project Options

Choose one of the following tracks:

### 📊 Data Analysis Pipeline
Build a complete data processing and analysis pipeline for a research domain of your choice.

**Requirements:**
- Data ingestion from multiple sources
- Cleaning and preprocessing workflows
- Statistical analysis and visualization
- Automated report generation
- Configuration-driven processing

### 🧮 Scientific Computing Tool
Develop a computational tool for scientific calculations or simulations.

**Requirements:**
- Mathematical modeling implementation
- Performance optimization
- Numerical accuracy validation
- Interactive user interface
- Comprehensive documentation

### 🔬 Research Workflow Manager
Create a tool to manage and automate research workflows.

**Requirements:**
- Task dependency management
- Progress tracking and logging
- Configuration management
- Integration with existing tools
- Web-based dashboard

### 💡 Custom Project
Propose your own research software project (requires instructor approval).

**Proposal Requirements:**
- Problem statement and motivation
- Technical approach and architecture
- Timeline and milestones
- Success criteria and evaluation

## Technical Requirements

### Core Implementation (120 points)
- **Architecture**: Clean, modular design with clear separation of concerns
- **Functionality**: All core features implemented and working
- **Performance**: Efficient algorithms and optimized execution
- **Error Handling**: Robust error handling and user feedback
- **Configuration**: Flexible configuration system

### Testing & Quality (60 points)
- **Unit Tests**: Comprehensive test coverage (>85%)
- **Integration Tests**: End-to-end workflow testing
- **Performance Tests**: Benchmarking and profiling
- **Code Quality**: Clean, readable, maintainable code
- **Documentation**: API docs, user guides, developer docs

### Reproducibility (60 points)
- **Environment**: Containerized or virtual environment setup
- **Dependencies**: Clear dependency management
- **Data**: Sample datasets and data provenance
- **Workflows**: Automated build and test pipelines
- **Results**: Reproducible outputs and analysis

### Collaboration (30 points)
- **Version Control**: Effective Git workflow and history
- **Code Review**: Pull request process and peer review
- **Communication**: Clear commit messages and documentation
- **Project Management**: Issue tracking and milestone planning

### Presentation (30 points)
- **Demo**: Live demonstration of your software
- **Documentation**: Comprehensive project documentation
- **Reflection**: Critical analysis of design decisions
- **Impact**: Discussion of potential research applications

## Deliverables

### Week 1: Project Proposal
- Problem statement and research context
- Technical approach and architecture diagram
- Timeline with milestones
- Team formation (if applicable)

### Week 2: Initial Implementation
- Core functionality prototype
- Basic test suite
- Documentation outline
- Continuous integration setup

### Week 3: Feature Complete
- All core features implemented
- Comprehensive testing
- Performance optimization
- User documentation

### Week 4: Final Submission
- Complete software package
- Deployment instructions
- Final presentation
- Project reflection

## Repository Structure

```
final-project/
├── src/                    # Source code
├── tests/                  # Test suite
├── docs/                   # Documentation
├── data/                   # Sample datasets
├── configs/                # Configuration files
├── scripts/                # Utility scripts
├── .github/workflows/      # CI/CD pipelines
├── Dockerfile             # Container setup
├── requirements.txt       # Dependencies
├── setup.py              # Package installation
├── README.md             # Project overview
└── CONTRIBUTING.md       # Development guide
```

## Evaluation Criteria

### Technical Excellence (40%)
- Code quality and architecture
- Performance and efficiency
- Testing and reliability
- Documentation quality

### Research Impact (25%)
- Problem significance
- Solution effectiveness
- Reproducibility
- Potential for reuse

### Software Engineering (25%)
- Development process
- Collaboration effectiveness
- Version control usage
- Project management

### Communication (10%)
- Presentation quality
- Documentation clarity
- Code readability
- Team communication

## Resources

- **GitHub Classroom**: Project repositories and submission
- **Documentation Tools**: Sphinx, MkDocs, or GitBook
- **CI/CD**: GitHub Actions or GitLab CI
- **Containerization**: Docker and docker-compose
- **Testing**: pytest, unittest, or language-specific frameworks

## Getting Help

- **Weekly Check-ins**: Scheduled progress meetings
- **Office Hours**: Extended hours during project period
- **Peer Review**: Code review sessions with classmates
- **Technical Support**: Infrastructure and tooling assistance

---

*Due: {{ page.due_date | date: "%B %d, %Y at %I:%M %p" }} • Points: {{ page.points }} • Team Size: {{ page.team_size }}*