---
layout: project
title: "ECONGAMES: Monte-Carlo Game-Theory Toolkit"
team: ["Marco Rossi", "Julie Dubois", "Ahmed Hassan", "Lisa Wang"]
course_year: "2025"
project_type: "Final Project"
featured: false
summary: "A comprehensive toolkit for simulating and analyzing game-theoretic scenarios using Monte Carlo methods, with focus on economic equilibria and strategic behavior analysis."
technologies:
  - "Python 3.11"
  - "NumPy"
  - "NetworkX"
  - "Plotly"
  - "FastAPI"
  - "Pydantic"
  - "pytest"
tags:
  - "Game Theory"
  - "Economics"
  - "Monte Carlo"
  - "Network Analysis"
github_url: "https://github.com/marcorossi/econgames-toolkit"
demo_url: "https://econgames-api.herokuapp.com"
documentation_url: "https://marcorossi.github.io/econgames-toolkit"
---

## Overview

ECONGAMES is a sophisticated Monte Carlo simulation toolkit designed for analyzing game-theoretic scenarios in economics. The project provides researchers and students with powerful tools to simulate strategic interactions, find equilibria, and analyze the stability of economic systems under uncertainty.

## Problem Statement

Economic researchers need computational tools to:
- Simulate complex multi-player games with stochastic elements
- Find and verify Nash equilibria in large strategy spaces
- Analyze evolutionary stable strategies under uncertainty
- Model network effects in economic interactions

Traditional analytical methods become intractable for games with many players or complex strategy spaces, requiring computational approaches.

## Key Features

### 🎮 Game Types Supported
- **Normal Form Games**: Classic matrix games with n players
- **Extensive Form Games**: Sequential games with perfect/imperfect information
- **Evolutionary Games**: Population dynamics and ESS analysis
- **Network Games**: Strategic interactions on graphs

### 🔬 Analysis Tools
- **Equilibrium Finding**: Multiple algorithms for Nash equilibria
- **Monte Carlo Simulation**: Stochastic strategy evolution
- **Stability Analysis**: Perturbation testing of equilibria
- **Convergence Analysis**: Strategy learning dynamics

### 📊 Visualization
- **Strategy Dynamics**: Animated evolution of player strategies
- **Payoff Landscapes**: 3D visualization of game outcomes
- **Network Visualization**: Interactive graph-based games
- **Statistical Plots**: Distribution of outcomes and convergence

## Technical Implementation

### Core Game Engine
```python
class Game:
    """Base class for all game types."""
    
    def __init__(self, players: List[Player], payoff_functions: Dict):
        self.players = players
        self.payoff_functions = payoff_functions
        
    def simulate_round(self, strategies: Dict[str, Strategy]) -> Dict[str, float]:
        """Simulate one round of the game."""
        payoffs = {}
        for player in self.players:
            payoffs[player.id] = self.calculate_payoff(player, strategies)
        return payoffs
        
    def find_nash_equilibria(self, method: str = "iterative") -> List[StrategyProfile]:
        """Find Nash equilibria using specified method."""
        if method == "iterative":
            return self._iterative_best_response()
        elif method == "evolutionary":
            return self._evolutionary_stable_strategy()
```

### Monte Carlo Simulation Engine
```python
class MonteCarloSimulator:
    def __init__(self, game: Game, n_simulations: int = 10000):
        self.game = game
        self.n_simulations = n_simulations
        
    def run_evolution_simulation(self, 
                                initial_population: Population,
                                mutation_rate: float = 0.01) -> SimulationResults:
        """Run evolutionary game simulation."""
        results = []
        population = initial_population.copy()
        
        for generation in range(self.n_simulations):
            # Play games and collect payoffs
            payoffs = self._play_population_games(population)
            
            # Update strategies based on success
            population = self._update_population(population, payoffs, mutation_rate)
            
            # Record results
            results.append(self._analyze_population(population))
            
        return SimulationResults(results)
```

## Project Highlights

### 📈 Performance Optimizations
- **Vectorized Computations**: NumPy-based matrix operations for large games
- **Parallel Processing**: Multiprocessing for independent simulations
- **Caching**: Memoization of expensive equilibrium calculations
- **Sparse Representations**: Efficient storage for large strategy spaces

### 🧠 Advanced Algorithms
- **Lemke-Howson Algorithm**: Exact Nash equilibrium finding
- **Evolutionary Stable Strategy**: Population dynamics simulation
- **Fictitious Play**: Adaptive learning algorithms
- **Quantal Response Equilibrium**: Bounded rationality models

### 🌐 API Design
- **RESTful API**: FastAPI-based web service
- **Interactive Documentation**: Auto-generated Swagger UI
- **Validation**: Pydantic models for type safety
- **Async Support**: Concurrent simulation handling

## Use Cases and Examples

### Example 1: Prisoner's Dilemma Tournament
```python
# Set up classic Prisoner's Dilemma
pd_game = NormalFormGame(
    players=["Alice", "Bob"],
    strategies={"Alice": ["Cooperate", "Defect"], 
               "Bob": ["Cooperate", "Defect"]},
    payoffs={
        ("Cooperate", "Cooperate"): (3, 3),
        ("Cooperate", "Defect"): (0, 5),
        ("Defect", "Cooperate"): (5, 0),
        ("Defect", "Defect"): (1, 1)
    }
)

# Run tournament with different strategies
tournament = Tournament(pd_game)
results = tournament.run_round_robin(strategies=[
    "TitForTat", "AlwaysDefect", "AlwaysCooperate", "Random"
])
```

### Example 2: Network Market Competition
```python
# Model competition on a social network
network = nx.barabasi_albert_graph(n=100, m=3)
market_game = NetworkGame(
    network=network,
    player_types=["Firm", "Consumer"],
    interaction_rules=local_competition_rules
)

# Simulate market dynamics
simulator = MonteCarloSimulator(market_game, n_simulations=5000)
results = simulator.run_network_evolution(
    initial_strategies=random_strategies,
    learning_rate=0.1
)
```

## Testing and Validation

### Mathematical Validation
- **Known Equilibria**: Verified against analytical solutions
- **Convergence Properties**: Tested convergence to known results
- **Boundary Conditions**: Edge case validation
- **Numerical Precision**: Floating-point stability testing

### Performance Testing
- **Scalability Tests**: Games with up to 1000 players
- **Memory Usage**: Profiling for large strategy spaces
- **Execution Time**: Benchmarking against theoretical complexity
- **Parallel Efficiency**: Speedup measurement for concurrent simulations

## Team Collaboration

### Development Workflow
- **Agile Methodology**: 2-week sprints with retrospectives
- **Feature Branches**: Git flow with code review
- **Continuous Integration**: Automated testing and deployment
- **Documentation**: Sphinx with mathematical notation support

### Specialization Areas
- **Marco**: Core game engine and equilibrium algorithms
- **Julie**: Monte Carlo simulation and statistical analysis
- **Ahmed**: Network games and graph algorithms
- **Lisa**: API development and user interface

## Academic Applications

The toolkit has been used for:
- **Course Projects**: Game theory assignments in Economics courses
- **Research Papers**: Analysis of market competition dynamics
- **Policy Analysis**: Simulation of regulatory interventions
- **Educational Tools**: Interactive demonstrations for lectures

## Industry Relevance

### Real-World Applications
- **Auction Design**: Bidding strategy analysis
- **Market Analysis**: Competitive dynamics simulation
- **Mechanism Design**: Incentive structure optimization
- **Behavioral Economics**: Bounded rationality modeling

### Compliance and Standards
- **Reproducible Research**: Deterministic random seeds
- **Data Formats**: Standard input/output formats
- **Documentation**: IEEE documentation standards
- **Code Quality**: PEP 8 compliance with type hints

## Future Development

### Planned Features
1. **Machine Learning Integration**: Deep reinforcement learning agents
2. **Bayesian Games**: Incomplete information handling
3. **Mechanism Design Tools**: Auction and voting system design
4. **Real-time Simulation**: Live multi-player game interfaces

### Research Directions
- **Quantum Game Theory**: Extension to quantum strategic interactions
- **Behavioral Models**: Integration of psychological factors
- **Large-scale Simulations**: Distributed computing for massive games
- **AI Opponents**: Integration with modern AI game-playing agents

## Lessons Learned

### Technical Challenges
- **Numerical Stability**: Floating-point precision in equilibrium calculations
- **Scalability**: Memory management for large games
- **Algorithm Selection**: Trade-offs between accuracy and performance

### Software Engineering
- **API Design**: Balancing flexibility with ease of use
- **Testing Strategy**: Validating stochastic algorithms
- **Documentation**: Explaining complex mathematical concepts clearly

---

*ECONGAMES demonstrates the intersection of economic theory, advanced algorithms, and software engineering, providing a robust foundation for computational game theory research.*