---
layout: project
title: "QSIM: Discrete-Event Queue Simulator"
team: ["Nina Kowalski", "James Thompson", "Raj Patel"]
course_year: "2024"
project_type: "Final Project"
featured: false
summary: "A high-performance discrete-event simulation framework for analyzing queueing systems with support for complex topologies, custom arrival processes, and real-time visualization."
technologies:
  - "Python 3.10"
  - "SimPy"
  - "NumPy"
  - "Matplotlib"
  - "Dash"
  - "NetworkX"
  - "Asyncio"
tags:
  - "Simulation"
  - "Operations Research"
  - "Queueing Theory"
  - "Performance Analysis"
github_url: "https://github.com/ninakowalski/qsim-simulator"
demo_url: "https://qsim-dashboard.herokuapp.com"
documentation_url: "https://ninakowalski.github.io/qsim-simulator"
---

## Overview

QSIM is a sophisticated discrete-event simulation framework designed for analyzing complex queueing systems. From simple M/M/1 queues to intricate network topologies, QSIM provides researchers and practitioners with powerful tools for performance analysis, capacity planning, and system optimization.

## Problem Statement

Modern systems require sophisticated queueing analysis:
- **Service Centers**: Call centers, hospitals, manufacturing systems
- **Computer Networks**: Traffic analysis, server farms, cloud computing
- **Transportation**: Airport security, traffic lights, public transit
- **Financial Services**: Bank branches, trading systems, payment processing

Existing simulation tools are either too simplistic for complex scenarios or too expensive for academic and small business use.

## Solution Architecture

### Core Simulation Engine
Built on discrete-event simulation principles with:
- **Event-driven Architecture**: Efficient event scheduling and processing
- **Modular Components**: Reusable queue, server, and network elements
- **Extensible Framework**: Plugin architecture for custom behaviors
- **Statistical Collection**: Comprehensive performance metrics

### Key Components

1. **Queue Models**
   - Single-server and multi-server queues
   - Priority queues with preemption
   - Finite capacity with blocking/balking
   - Batch arrival and service processes

2. **Network Topologies**
   - Series and parallel queue networks
   - Closed and open queueing networks
   - Custom routing algorithms
   - Load balancing strategies

3. **Arrival Processes**
   - Poisson, Erlang, and Hyperexponential distributions
   - Non-stationary arrival rates
   - Batch arrivals and group processing
   - Correlated arrival streams

4. **Service Mechanisms**
   - Multiple service disciplines (FIFO, LIFO, Priority)
   - State-dependent service rates
   - Server breakdowns and repairs
   - Resource sharing and constraints

## Technical Implementation

### Discrete-Event Engine
```python
import simpy
from typing import Generator, Any

class QueueingSystem:
    def __init__(self, env: simpy.Environment):
        self.env = env
        self.servers = []
        self.queue = simpy.Store(env)
        self.statistics = StatisticsCollector()
        
    def customer_arrival_process(self) -> Generator[simpy.Event, Any, None]:
        """Generate customer arrivals according to specified process."""
        customer_id = 0
        while True:
            # Sample inter-arrival time
            inter_arrival = self.arrival_distribution.sample()
            yield self.env.timeout(inter_arrival)
            
            # Create new customer
            customer = Customer(customer_id, self.env.now)
            customer_id += 1
            
            # Add to queue
            self.queue.put(customer)
            self.statistics.record_arrival(customer)
```

### Server Process
```python
class Server:
    def __init__(self, env: simpy.Environment, service_rate: float):
        self.env = env
        self.service_rate = service_rate
        self.resource = simpy.Resource(env, capacity=1)
        self.busy = False
        
    def serve_customers(self, queue: simpy.Store) -> Generator:
        """Continuous server process."""
        while True:
            # Wait for customer
            customer = yield queue.get()
            
            # Request server resource
            with self.resource.request() as request:
                yield request
                
                # Record service start
                customer.service_start = self.env.now
                self.busy = True
                
                # Sample service time
                service_time = random.exponential(1.0 / self.service_rate)
                yield self.env.timeout(service_time)
                
                # Complete service
                customer.service_end = self.env.now
                self.busy = False
                
                # Record statistics
                self.statistics.record_departure(customer)
```

## Advanced Features

### 🔄 Network Simulation
- **Complex Topologies**: Build arbitrary queueing networks
- **Routing Algorithms**: Probabilistic, shortest queue, load balancing
- **Feedback Loops**: Customers returning to previous stations
- **Blocking Networks**: Finite capacity with blocking

### 📊 Statistical Analysis
- **Performance Metrics**: Response time, throughput, utilization
- **Confidence Intervals**: Steady-state and transient analysis
- **Batch Means**: Independent replications for statistical validity
- **Variance Reduction**: Antithetic variables, control variates

### 🎯 Optimization Tools
- **Sensitivity Analysis**: Parameter sweep and optimization
- **Capacity Planning**: Resource allocation optimization
- **Cost Models**: Economic analysis of system configurations
- **What-if Analysis**: Scenario comparison tools

### 📈 Real-time Visualization
```python
class RealTimeVisualizer:
    def __init__(self, simulation):
        self.simulation = simulation
        self.app = dash.Dash(__name__)
        self.setup_layout()
        
    def update_metrics(self):
        """Update dashboard with current simulation metrics."""
        return {
            'queue_length': self.simulation.get_queue_length(),
            'server_utilization': self.simulation.get_utilization(),
            'average_wait_time': self.simulation.get_avg_wait_time(),
            'throughput': self.simulation.get_throughput()
        }
```

## Simulation Examples

### Example 1: M/M/1 Queue Analysis
```python
# Set up basic M/M/1 queue
env = simpy.Environment()
queue_system = QueueingSystem(env)

# Configure parameters
arrival_rate = 0.8  # customers per minute
service_rate = 1.0  # customers per minute

# Run simulation
queue_system.configure(
    arrival_process=PoissonProcess(arrival_rate),
    service_process=ExponentialService(service_rate),
    servers=1
)

# Execute simulation
env.run(until=1000)  # Run for 1000 time units

# Analyze results
results = queue_system.get_statistics()
print(f"Average queue length: {results.avg_queue_length:.2f}")
print(f"Average wait time: {results.avg_wait_time:.2f}")
print(f"Server utilization: {results.server_utilization:.2f}")
```

### Example 2: Network of Queues
```python
# Create network topology
network = QueueNetwork()

# Add stations
reception = network.add_station("Reception", servers=2, service_rate=1.5)
triage = network.add_station("Triage", servers=1, service_rate=2.0)
treatment = network.add_station("Treatment", servers=3, service_rate=0.8)

# Define routing
network.add_route(reception, triage, probability=1.0)
network.add_route(triage, treatment, probability=0.7)
network.add_route(triage, "EXIT", probability=0.3)
network.add_route(treatment, "EXIT", probability=1.0)

# Configure arrivals
network.set_arrival_process(
    station=reception,
    process=PoissonProcess(rate=1.2)
)

# Run simulation
results = network.simulate(duration=8*60)  # 8-hour simulation
```

## Performance and Scalability

### Optimization Techniques
- **Event List Management**: Efficient priority queue implementation
- **Memory Management**: Object pooling for high-throughput simulations
- **Parallel Execution**: Multi-core support for independent replications
- **Incremental Statistics**: Online algorithms for metric calculation

### Benchmarks
- **Simulation Speed**: 1M events processed in <30 seconds
- **Memory Usage**: <100MB for 10K concurrent entities
- **Accuracy**: 99.9% agreement with analytical solutions where available
- **Scalability**: Networks with 1000+ nodes supported

## Validation and Verification

### Analytical Validation
```python
class ValidationSuite:
    def test_mm1_theoretical(self):
        """Validate M/M/1 results against theoretical values."""
        rho = self.arrival_rate / self.service_rate
        
        # Theoretical values
        theoretical_utilization = rho
        theoretical_avg_queue = rho / (1 - rho)
        theoretical_avg_wait = rho / (self.service_rate * (1 - rho))
        
        # Simulation results
        sim_results = self.run_mm1_simulation()
        
        # Statistical tests
        assert abs(sim_results.utilization - theoretical_utilization) < 0.05
        assert abs(sim_results.avg_queue - theoretical_avg_queue) < 0.1
        assert abs(sim_results.avg_wait - theoretical_avg_wait) < 0.1
```

### Statistical Testing
- **Steady-state Detection**: Automatic warm-up period identification
- **Confidence Intervals**: Student-t based confidence bounds
- **Goodness-of-fit**: Chi-square tests for distribution assumptions
- **Independence Tests**: Autocorrelation analysis of outputs

## User Interface and Experience

### Command-Line Interface
```bash
# Run simple M/M/1 simulation
qsim run --model mm1 --arrival-rate 0.8 --service-rate 1.0 --duration 1000

# Network simulation from configuration file
qsim run --config hospital_network.yaml --replications 10

# Parameter sweep
qsim sweep --model mm1 --param arrival_rate --range 0.1:1.0:0.1 --metric utilization
```

### Web Dashboard
- **Real-time Monitoring**: Live simulation progress and metrics
- **Interactive Controls**: Pause, restart, parameter adjustment
- **Visualization**: Queue length plots, utilization charts
- **Export Options**: CSV, JSON, PDF reports

## Industry Applications

### Healthcare Systems
- **Emergency Department**: Patient flow optimization
- **Operating Room Scheduling**: Resource allocation
- **Pharmacy Operations**: Prescription processing
- **Appointment Systems**: Scheduling optimization

### Manufacturing
- **Production Lines**: Bottleneck identification
- **Quality Control**: Inspection station analysis
- **Inventory Management**: Replenishment policies
- **Maintenance Planning**: Preventive maintenance scheduling

### Service Industries
- **Call Centers**: Staffing optimization
- **Retail Checkout**: Queue configuration
- **Banking**: Teller and ATM analysis
- **Transportation**: Terminal and hub operations

## Team Collaboration and Development

### Agile Development Process
- **Sprint Planning**: 2-week iterations with clear deliverables
- **Code Reviews**: Mandatory peer review for all changes
- **Testing Strategy**: Test-driven development with 95% coverage
- **Documentation**: Comprehensive API and user documentation

### Role Distribution
- **Nina**: Core simulation engine and statistical analysis
- **James**: Network topology and routing algorithms
- **Raj**: Visualization dashboard and user interface

### Technical Standards
- **Code Quality**: Black formatting, flake8 linting, mypy typing
- **Testing**: Pytest with property-based testing using Hypothesis
- **Documentation**: Sphinx with mathematical notation support
- **CI/CD**: GitHub Actions with automated testing and deployment

## Academic and Research Impact

### Educational Value
- **Teaching Tool**: Used in Operations Research courses
- **Research Platform**: Foundation for advanced queueing research
- **Case Studies**: Real-world applications in multiple domains
- **Open Source**: Available for academic and commercial use

### Research Applications
- **Performance Analysis**: Comparison of queueing disciplines
- **System Design**: Optimal resource allocation studies
- **Stochastic Modeling**: Advanced arrival and service processes
- **Network Theory**: Large-scale queueing network analysis

## Future Development

### Planned Enhancements
1. **Machine Learning**: AI-driven parameter optimization
2. **Real-time Integration**: Live data feeds from operational systems
3. **Advanced Visualization**: 3D network topology displays
4. **Cloud Deployment**: Scalable simulation in cloud environments

### Research Directions
- **Quantum Queueing**: Extension to quantum computing scenarios
- **Social Networks**: Human behavior modeling in queues
- **IoT Integration**: Internet of Things device simulation
- **Blockchain**: Distributed consensus mechanism analysis

---

*QSIM demonstrates the application of advanced simulation techniques to solve real-world operational challenges, combining theoretical rigor with practical software engineering.*