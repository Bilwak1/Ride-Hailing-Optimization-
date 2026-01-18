# Ride Hailing Optimization System

A Gurobi-based optimization model for intelligent taxi dispatch decisions in New York City, considering real-world constraints such as traffic, legal zones, driver capacity, and operational costs.

## 📋 Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Problem Formulation](#problem-formulation)
- [Installation](#installation)
- [Data Requirements](#data-requirements)
- [Usage](#usage)
- [Results](#results)
- [Future Scope](#future-scope)
- [Team](#team)
- [License](#license)

## 🎯 Overview

This project optimizes real-time dispatching of NYC Yellow and Green taxis to passenger requests using historical trip data. Unlike simplistic nearest-cab algorithms, our model considers multiple factors including:

- **Regulatory Constraints**: Green cab restrictions in Manhattan south of 96th Street
- **Capacity Matching**: Passenger count vs. vehicle capacity
- **Profit Optimization**: Maximizing net profit after fuel costs
- **Wait Time Minimization**: Balancing customer satisfaction with profitability
- **Real-World Traffic**: Using Google Maps API for accurate ETAs

## ✨ Features

- **Multi-Objective Optimization**: Balances profit maximization and wait time minimization
- **Regulatory Compliance**: Enforces NYC TLC zone restrictions for green taxis
- **Traffic-Aware**: Integrates Google Maps Distance Matrix API for real-time ETAs
- **Cost Calculation**: Accounts for fuel costs based on vehicle type and distance
- **Interactive Visualization**: Folium maps showing cab-guest assignments
- **Constraint Validation**: Ensures capacity, zone, and assignment feasibility

## 📐 Problem Formulation

### Decision Variables
- **X<sub>cg</sub>**: Binary variable (1 if cab *c* is assigned to guest *g*, 0 otherwise)

### Objective Functions
1. **Maximize Total Profit**: MAX Σ(Profit<sub>cg</sub> × X<sub>cg</sub>)
2. **Minimize Wait Times**: MIN Σ(ETA<sub>cg</sub> × X<sub>cg</sub>)

### Constraints
- **Capacity Constraint**: X<sub>cg</sub> = 0 if passenger count > cab capacity
- **One Ride per Cab**: Σ<sub>g</sub> X<sub>cg</sub> ≤ 1 for each cab
- **One Cab per Guest**: Σ<sub>c</sub> X<sub>cg</sub> = 1 for each guest
- **Green Cab Zone Restriction**: X<sub>cg</sub> = 0 if green cab and guest in restricted zone

### Weighted Optimization
- Profit priority weight: 15
- Wait time priority weight: 5

## 🔧 Installation

### Prerequisites
- Python 3.8+
- Gurobi Optimizer (with valid license)
- Google Maps API key

### Setup

1. Clone the repository:
```bash
git clone https://github.com/yourusername/ride-hailing-optimization.git
cd ride-hailing-optimization
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Set up your Google Maps API key:
   - Replace `API_KEY` in the notebook with your key
   - Or set as environment variable: `export GOOGLE_MAPS_API_KEY='your_key_here'`

4. Configure Gurobi:
   - Ensure you have a valid Gurobi license
   - Follow [Gurobi installation guide](https://www.gurobi.com/documentation/)

## 📊 Data Requirements

### Input Files
- `supply.csv`: Available cab data (location, type, capacity)
- `demand.csv`: Ride requests (pickup/dropoff locations, passenger count, fare)

### Data Sources
- **NYC Open Data**: 2016 Yellow & Green Taxi Trip Records
- **Google Maps Distance Matrix API**: Real-time ETA and distances

### Simulation Setup
- **Demand**: Trips requested 8:00-8:05 PM, January 1, 2016
- **Supply**: Trips ending 7:55-8:00 PM, January 1, 2016

## 🚀 Usage

### Running the Optimization

1. Open the Jupyter notebook:
```bash
jupyter notebook Ride_Hailing_Optimization.ipynb
```

2. Execute cells sequentially to:
   - Load and preprocess data
   - Calculate ETAs and profits
   - Build Gurobi optimization model
   - Solve and visualize assignments

### Key Parameters

Modify these in the notebook:
```python
# Fuel pricing
gas_price = 3.650  # $/gallon

# Vehicle efficiency
mpg_lookup = {
    ('yellow', 'sedan'): 45,
    ('yellow', 'suv'): 25,
    ('green', 'sedan'): 45,
    ('green', 'suv'): 28
}

# Objective weights
profit_weight = 15
wait_time_weight = 5
```

## 📈 Results

### Sample Assignments
- Guest32 → Cab218
- Guest19 → Cab289
- Guest254 → Cab240
- Guest179 → Cab132
- Guest56 → Cab8
- Guest30 → Cab260

### Validation Example
**Guest179 Assignment Analysis:**

| Factor | Cab14 (Rejected) | Cab132 (Selected) |
|--------|------------------|-------------------|
| ETA | 469 sec | 778 sec |
| Profit | $6.80 | $6.52 |
| Capacity | 4 seats | 5 seats |
| **Guest Requirement** | **5 seats** | **5 seats** |

**Result**: Cab14 rejected due to insufficient capacity, demonstrating the model's constraint enforcement.

## 🔮 Future Scope

### Enhancements
- **Real-Time Dynamic Dispatching**: Live updates for new requests
- **Ride Pooling**: Shared rides for cost reduction
- **Demand Forecasting**: Predictive cab repositioning
- **Reinforcement Learning**: Adaptive decision-making
- **API Integration**: Production-ready backend service
- **Live Traffic Integration**: Real-time route adjustments

### Cross-Industry Applications
- **Logistics & Delivery**: Route optimization for FedEx, Amazon
- **Emergency Response**: Ambulance/fire unit dispatch
- **Field Services**: Technician scheduling
- **Event Staffing**: Resource allocation

## 👥 Team

**Group 6:**
- Kai Yang
- Bilwa Khaparde
- Linh Tran
- Sangita Poudel
- Rifa Safeer Shah

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- NYC Taxi & Limousine Commission for open data
- Google Maps Platform for API services
- Gurobi Optimization for solver technology

## 📞 Contact

For questions or collaboration opportunities, please open an issue on GitHub.

---

**Note**: This project is for educational purposes. For production use, ensure compliance with all applicable regulations and obtain necessary licenses.
