Ride Hailing Optimization (NYC Taxi Dispatch)
Project Overview
This project addresses the real-time dispatching challenge in New York City by moving beyond simple "nearest-neighbor" assignments to a global optimization model. Using a combination of NYC Taxi data and the Google Maps Distance Matrix API, we developed a Gurobi-based binary integer programming model to intelligently match passengers with the most suitable cabs.

Key Features
Profit Maximization: Optimizes total net profit by factoring in fare revenue against operational costs (fuel efficiency and travel distance).

Regulatory Constraints: Implements NYC-specific legal restrictions, such as prohibiting "Green Taxis" from street pickups in Manhattan below 96th Street.

Capacity Matching: Ensures vehicle passenger capacity meets the specific demand of each guest request.

Traffic-Aware Routing: Uses Google Maps API to pull real-time ETAs and distances for more accurate decision-making.

Visual Analysis: Includes an interactive Folium map to visualize the spatial distribution of cabs, guests, and the final assignments.

Tech Stack
Optimization: Gurobi (gurobipy)

Data Processing: Pandas, NumPy, Scikit-learn

APIs: Google Maps Distance Matrix API

Visualization: Folium, Leaflet

Environment: Jupyter Notebook

Getting Started
Prerequisites

Gurobi License: A valid Gurobi license is required to run the optimization model.

Google Maps API Key: You will need an API key with the "Distance Matrix API" enabled.

Installation

Clone the repository:

Bash
git clone https://github.com/your-username/ride-hailing-optimization.git
Install dependencies:

Bash
pip install pandas scikit-learn googlemaps gurobipy folium
How to Run

Ensure supply.csv and demand.csv are in the project root directory.

Open codes.ipynb in your Jupyter environment.

Add your Google Maps API key to the designated variable in the code.

Run the cells to see the optimization results and the interactive map.

Contributors
Kai Yang

Bilwa Khaparde

Linh Tran

Sangita Poudel

Rifa Safeer Shah

License
This project was developed for educational purposes. Please contact the contributors for licensing or usage permissions.
