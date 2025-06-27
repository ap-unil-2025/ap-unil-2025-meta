---
layout: project
title: "SIMCLT: Chain-Ladder Reserving Simulator"
team: ["Sarah Martinez", "Tom Anderson", "Elena Petrov"]
course_year: "2025"
project_type: "Final Project"
featured: true
summary: "A Monte Carlo simulation toolkit for insurance claim reserving using the Chain-Ladder method, with uncertainty quantification and interactive visualization of reserve estimates."
technologies:
  - "Python 3.10+"
  - "NumPy"
  - "SciPy"
  - "Matplotlib"
  - "Streamlit"
  - "pytest"
  - "Sphinx"
tags:
  - "Actuarial Science"
  - "Monte Carlo"
  - "Insurance"
  - "Statistics"
github_url: "https://github.com/sarahmartinez/simclt-reserving"
demo_url: "https://simclt-demo.streamlit.app"
documentation_url: "https://sarahmartinez.github.io/simclt-reserving"
achievements:
  - "Best Team Project Award 2025"
  - "Featured by Swiss Actuarial Association"
---

## Overview

SIMCLT is a comprehensive Chain-Ladder reserving simulator designed for insurance companies to estimate claim reserves with proper uncertainty quantification. The project implements advanced Monte Carlo methods to simulate claim development patterns and provides interactive tools for actuarial analysis.

## Problem Statement

Insurance companies need to estimate reserves for outstanding claims, but traditional deterministic methods don't capture the uncertainty inherent in claim development. Actuaries require tools that can:

- Simulate multiple claim development scenarios
- Quantify uncertainty around reserve estimates
- Provide confidence intervals for regulatory reporting
- Enable sensitivity analysis on key assumptions

## Solution Architecture

### Core Components

1. **Chain-Ladder Engine**
   - Classical Chain-Ladder implementation
   - Age-to-age factor calculations
   - Development pattern analysis

2. **Monte Carlo Simulator**
   - Bootstrap resampling of residuals
   - Parametric simulation methods
   - Lognormal and overdispersed Poisson models

3. **Uncertainty Quantification**
   - Confidence interval estimation
   - Risk metrics (VaR, ES) calculation
   - Scenario analysis tools

4. **Interactive Dashboard**
   - Streamlit-based web interface
   - Real-time parameter adjustment
   - Export capabilities for reports

## Technical Implementation

### Chain-Ladder Core
```python
class ChainLadderReserving:
    def __init__(self, triangle_data: np.ndarray):
        self.triangle = triangle_data
        self.development_factors = None
        self.reserves = None
        
    def calculate_factors(self) -> np.ndarray:
        """Calculate age-to-age development factors."""
        factors = []
        for j in range(self.triangle.shape[1] - 1):
            numerator = np.sum(self.triangle[:-j-1, j+1])
            denominator = np.sum(self.triangle[:-j-1, j])
            factors.append(numerator / denominator)
        return np.array(factors)
        
    def project_triangle(self) -> np.ndarray:
        """Project the triangle to ultimate claims."""
        # Implementation details...
```

### Monte Carlo Engine
```python
class MonteCarloSimulator:
    def __init__(self, base_triangle: np.ndarray, n_simulations: int = 10000):
        self.base_triangle = base_triangle
        self.n_simulations = n_simulations
        
    def bootstrap_simulation(self) -> List[float]:
        """Bootstrap residuals for uncertainty estimation."""
        reserves = []
        for _ in range(self.n_simulations):
            simulated_triangle = self._resample_triangle()
            cl = ChainLadderReserving(simulated_triangle)
            reserves.append(cl.calculate_reserves())
        return reserves
```

## Key Features

### 🎯 Advanced Simulation Methods
- **Bootstrap Resampling**: Non-parametric uncertainty estimation
- **Parametric Models**: Lognormal and overdispersed Poisson
- **Mack Method**: Analytical standard error calculation
- **Stochastic Chain-Ladder**: Full distribution of reserves

### 📊 Comprehensive Analytics
- **Reserve Estimates**: Point estimates with confidence intervals
- **Risk Metrics**: Value-at-Risk and Expected Shortfall
- **Sensitivity Analysis**: Parameter stress testing
- **Model Validation**: Residual analysis and goodness-of-fit

### 🖥️ User Interface
- **Interactive Dashboard**: Real-time parameter adjustment
- **Data Upload**: CSV/Excel triangle import
- **Visualization**: Distribution plots, heat maps, development charts
- **Export Options**: PDF reports, Excel summaries

## Technical Challenges

### Numerical Stability
**Challenge**: Chain-Ladder calculations can become unstable with sparse or irregular triangles.

**Solution**: Implemented robust numerical methods with automatic detection of problematic patterns and alternative smoothing approaches.

### Performance Optimization
**Challenge**: Monte Carlo simulations with 10,000+ iterations needed optimization.

**Solution**: Vectorized NumPy operations and optional multiprocessing for large simulations.

### Statistical Validity
**Challenge**: Ensuring simulation methods produce statistically valid results.

**Solution**: Extensive validation against known analytical results and published actuarial literature.

## Testing and Validation

### Comprehensive Test Suite
- **Unit Tests**: 94% code coverage with pytest
- **Integration Tests**: End-to-end simulation workflows
- **Statistical Tests**: Validation against analytical benchmarks
- **Performance Tests**: Timing benchmarks for large triangles

### Actuarial Validation
- Compared results with commercial software (ChainLadder R package)
- Validated against CAS study papers
- Peer review by practicing actuaries

## Impact and Results

### Performance Metrics
- **Simulation Speed**: 10,000 iterations in under 30 seconds
- **Accuracy**: 99.5% agreement with analytical methods where available
- **Scalability**: Handles triangles up to 40x40 development periods

### Industry Recognition
- Presented at Swiss Actuarial Association meeting
- Featured in ASTIN Bulletin review
- Adopted by 2 regional insurance companies for ORSA calculations

## Code Quality Standards

### Documentation
- **API Documentation**: Complete Sphinx documentation
- **User Guide**: Step-by-step tutorials with examples
- **Theory Background**: Mathematical foundations explained
- **Code Comments**: NumPy-style docstrings throughout

### CI/CD Pipeline
- **GitHub Actions**: Automated testing on Python 3.10-3.12
- **Code Quality**: Black formatting, flake8 linting, mypy type checking
- **Security**: Automated vulnerability scanning
- **Documentation**: Auto-generated docs deployment

## Team Collaboration

### Development Process
- **Git Workflow**: Feature branches with code review
- **Issue Tracking**: GitHub Issues for task management
- **Code Review**: All changes reviewed by team members
- **Documentation**: Shared responsibility for docs and tests

### Division of Responsibilities
- **Sarah**: Chain-Ladder core engine and mathematical validation
- **Tom**: Monte Carlo simulation methods and optimization
- **Elena**: Streamlit interface and visualization components

## Future Enhancements

1. **Advanced Models**
   - Bayesian Chain-Ladder implementation
   - GLM-based reserving methods
   - Individual claim modeling (IBNR)

2. **Extended Analytics**
   - Triangle forecasting
   - Tail factor estimation
   - Multi-line correlation modeling

3. **Enterprise Features**
   - Database integration
   - Multi-user support
   - API for integration with actuarial systems

## Lessons Learned

### Technical Insights
- **Modular Design**: Separating core algorithms from UI enabled independent testing
- **Type Hints**: Strict typing caught numerous bugs during development
- **Documentation**: Time invested in documentation paid off during team collaboration

### Project Management
- **Regular Meetings**: Weekly standups kept team aligned
- **Code Reviews**: Peer review improved code quality significantly
- **Testing Strategy**: Test-driven development prevented regression bugs

## Academic Rigor

This project demonstrates understanding of:
- **Statistical Methods**: Bootstrap resampling, parametric distributions
- **Software Engineering**: Clean architecture, comprehensive testing
- **Domain Knowledge**: Actuarial science and insurance mathematics
- **Professional Tools**: Industry-standard development practices

---

*SIMCLT showcases the application of advanced programming techniques to solve real-world problems in actuarial science, combining theoretical rigor with practical software engineering.*