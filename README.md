# Burrito Optimization Game - Automated Solver

An automated optimization script using **Python** and **Gurobi Optimizer** to solve the daily challenges of the Gurobi Burrito Game. This project formulates the truck placement and customer assignment problem as a Mixed-Integer Linear Program (MILP) to maximize net profit.

---

## Features

- **Automated Data Ingestion:** Dynamically loads round and day-specific CSV datasets (`demand_node`, `truck_node`, `demand_truck`, and `problem_data`).
- **Mathematical Optimization (MILP):** Utilizes `gurobipy` to model binary decisions for truck placement ($x$) and customer-to-truck assignments ($y$).
- **Financial Breakdown:** Computes and displays exact metrics post-optimization (Gross Revenue, Ingredient Costs, Truck Operating Costs, and Net Profit).
- **Map Visualization:** Generates graphical maps comparing initial locations with the optimal solution layout.

---

## Prerequisites

Make sure you have Python and Jupyter Notebook installed along with the required libraries:

```bash
pip install pandas gurobipy
```

*Note: A valid Gurobi license (commercial or free academic/restricted) is required to run the optimization model.*

---

## Usage

1. Download the CSV data files directly from the game by clicking the "download files" button.
2. Place your CSV data files in the same directory as the script (or ensure your working path matches the expected naming convention: `roundX-dayY_...`).
3. Update the `round_number` and `day_number` variables at the top of the script according to the challenge you want to solve:
    
    ```python
    round_number = 1
    day_number = 1
    ```
    
4. Run the script via Jupyter Notebook:
    
    ```bash
    Burrito Game Solution.ipynb
    ```
    

---

## Mathematical Formulation

The optimization problem is formulated as follows:

### Objective Function

Maximize the net profit (gross revenue minus ingredient and truck operating costs):

$$
\max \sum_{b \in B} \sum_{t \in T} (r - c) \cdot d_{bt} \cdot y_{bt} - \sum_{t \in T} p \cdot x_t
$$

### Constraints

1. **Single truck assignment per building:** Each building’s customers can be served by at most one truck.
    
$$
\sum_{t \in T} y_{bt} \le 1 \quad \forall b \in B
$$
    
2. **Truck presence requirement:** Customers can only go to a parking spot if a truck is actually parked there.
    
$$
y_{bt} \le x_t \quad \forall b \in B, \, \forall t \in T
$$
    
3. **Binary variables:**
    
$$
x_t \in \{0, 1\} \quad \forall t \in T
$$
    
$$
y_{bt} \in \{0, 1\} \quad \forall b \in B, \, \forall t \in T
$$
    
