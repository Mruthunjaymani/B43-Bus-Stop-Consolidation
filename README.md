## B43 Bus Stop Consolidation - Stochastic Optimization

This project develops a **stochastic optimization model** to improve bus operations on the **B43 bus route in Brooklyn** by identifying an optimal set of bus stops to retain while minimizing total passenger cost. The model explicitly accounts for **ridership uncertainty** and balances **in-vehicle travel time savings** against **passenger walking cost**.

---

## Problem Overview

The B43 bus route contains closely spaced stops that increase dwell time and reduce average operating speed. While removing stops can improve travel time, it also increases walking distance for passengers.  

The goal of this project is to determine **which stops to remove** such that the **total passenger cost** is minimized while ensuring the solution remains **robust to ridership variability**.

---

## Key Challenges

- Ridership varies by stop and by day  
- Stop removal reduces dwell time but increases walking cost  
- Deterministic optimization may fail under demand fluctuations  

To address this, the problem is modeled as a **scenario-based stochastic optimization**.

---

## Methodology

### 1. Ridership Uncertainty Modeling
- Ridership at each stop is randomized using a **triangular distribution**
- Parameters:
  - Minimum = 75% of base ridership
  - Mode = base ridership
  - Maximum = 125% of base ridership
- **10 independent scenarios** are generated to represent daily demand variability

---

### 2. Scenario-Based Optimization
- For each scenario, total passenger cost is computed as:
  - **In-vehicle travel time cost**
  - **Walking time cost**
- A single stop-retention decision is optimized **across all scenarios**
- Objective: **Minimize average total passenger cost across scenarios**

This ensures the selected set of stops performs well under different ridership realizations, not just the base case.

---

## Optimization Model

### Decision Variable
- Binary variable indicating whether a bus stop is **kept or removed**

### Objective
- Minimize average scenario cost = (In-vehicle travel time cost + Walking cost)

### Key Constraints
- Direction-specific optimization (Northbound and Southbound)
- Consistent stop selection across all scenarios
- Operational feasibility of remaining stops

---

## Results

After optimization:

### Stop Configuration
- **35 stops retained per direction**
  - Northbound: 35 stops
  - Southbound: 35 stops

---

### Operational Impact

**Northbound Direction**
- Travel time reduction: **2.30 minutes per trip**
- Cost savings: **$1,835 per weekday**

**Southbound Direction**
- Travel time reduction: **2.01 minutes per trip**
- Cost savings: **$1,104 per weekday**

---

## Key Insights

- Scenario-based optimization produces a **robust stop configuration** that performs well under demand uncertainty
- Travel time savings significantly outweigh added walking costs
- Direction-specific optimization captures asymmetric ridership patterns
- Deterministic solutions would overestimate performance and risk poor real-world outcomes

---

## Tools & Techniques

- Python
- Gurobi Optimizer
- Mixed Integer Linear Programming (MILP)
- Monte Carlo Simulation
- Triangular Distribution for demand modeling
- Excel / CSV data processing

---

## Conclusion

This project demonstrates how **stochastic optimization** can be applied to real-world transit planning problems. By incorporating demand uncertainty directly into the optimization process, the model delivers **robust, implementable bus stop consolidation decisions** that reduce passenger travel time and operational costs without sacrificing accessibility.

---

## Notes

- Optimization performed separately for Northbound and Southbound directions
- All results are weekday averages
- Cost values represent passenger time cost savings
