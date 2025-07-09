# Dynamic Pricing for Urban Parking Lots

**Capstone Project – Summer Analytics 2025**  
Hosted by: Consulting & Analytics Club × Pathway

---

## Objective

To design and implement an intelligent, real-time pricing engine for urban parking spaces that:
- Updates prices dynamically based on demand, congestion, queue length, vehicle type, and special conditions
- Starts from a base price of **$10**
- Maintains **smooth and bounded** price variations (between 0.5x to 2x base)
- (Optional) Recommends rerouting to nearby lots based on real-time availability and competitor prices

---

## Project Architecture

flowchart TD
    A[Raw Data (dataset.csv)] --> B[Data Preprocessing]
    B --> C1[Model 1: Linear Pricing]
    B --> C2[Model 2: Demand-Based Pricing]
    C1 --> D[Predicted Prices]
    C2 --> D
    D --> E[Bokeh Visualization]
    D --> F[Report/Output]
    B --> G{Optional: Pathway\nReal-Time Streaming}
    G --> B


## Models Implemented

### Model 1: Baseline Linear Pricing
A simple model where price increases linearly with occupancy.

**Formula Used:**
Price_t+1 = Price_t + α × (Occupancy / Capacity)

Used as a reference model
- Helps understand basic demand-response behavior

---

### Model 2: Demand-Based Pricing
A smarter model that uses multiple features to compute a "demand score" and adjust price accordingly.

**Demand Function:**
Demand = α × (Occupancy / Capacity)
+ β × QueueLength
- γ × Traffic
+ δ × IsSpecialDay
+ ε × VehicleTypeWeight

  
**Price Formula:**
Price = BasePrice × (1 + λ × NormalizedDemand)


Price is bounded between **$5** and **$20** (i.e., 0.5x to 2.0x of $10)  
Normalized demand ensures smooth price changes

---

### Model 3 (Optional): Competitive Pricing (Template Only)
- Adds location-based intelligence using latitude and longitude
- Incorporates nearby lot prices to adjust current lot pricing
- Suggests rerouting if overburdened

---

## Features Used

| Feature                 | Description                                 |
|-------------------------|---------------------------------------------|
| `Occupancy`             | Number of vehicles currently parked         |
| `Capacity`              | Maximum capacity of the lot                 |
| `QueueLength`           | Number of vehicles waiting to enter        |
| `TrafficConditionNearby` | Traffic level around the lot (Low/Med/High)|
| `IsSpecialDay`          | Indicates holidays/events (0 or 1)          |
| `VehicleType`           | car / bike / truck                         |
| `Latitude`, `Longitude` | Used for location-based logic               |

---

## Tools & Technologies

| Tool        | Purpose                            |
|-------------|------------------------------------|
| **Python**  | Core programming language          |
| **Pandas**  | Data manipulation and processing   |
| **Numpy**   | Numerical operations               |
| **Bokeh**   | Real-time interactive visualizations|
| **Pathway** | (Optional) Real-time stream processing engine |

---

## Visualization

Using **Bokeh**, we generated:
- Real-time line plots for **Model 1 vs Model 2** prices
- Individual plots for each parking lot based on `'ID'`
- Clear legends and color-coded models

---

## Project Structure

DynamicParkingPricing/
│
├── dataset.csv # Source data (14 parking lots, 73 days)
├── main.ipynb # Google Colab notebook with complete code
├── README.md # This file
├── report.pdf # Explanation of methodology and results
└── bokeh_plots/ # (Optional) Exported HTML or images



---

## How to Run the Project

1. Open `Dynamic Pricing for Urban Parking Lots.ipynb` in **Google Colab** or Jupyter Notebook
2. Upload the provided `dataset.csv`
3. Run all cells:
   - Step-by-step model implementation
   - Real-time visualization with Bokeh

Final output: Real-time pricing graphs and stored model outputs for each parking lot

---


## Assumptions Made

- Traffic levels are mapped: `"Low"=1`, `"Medium"=2`, `"High"=3`
- Vehicle types are weighted: `car=1.0`, `bike=0.5`, `truck=1.5`
- Prices cannot fall below **$5** or rise above **$20**
- All models are built **from scratch** using only allowed libraries

---

## Deliverables Summary

- [x] Google Colab notebook with Model 1 & Model 2
- [x] Demand function explanation and assumptions
- [x] Smooth and explainable pricing variation
- [x] Real-time Bokeh plots
- [x] This README.md file
- [x] PDF Report (with methodology + screenshots)

---

## Resources

- [Pathway Docs – First Real-Time App](https://pathway.com/developers/user-guide/introduction/first_realtime_app_with_pathway/)
- [Summer Analytics 2025 Portal](https://www.caciitg.com/sa/course25/)
- [Bokeh Documentation](https://docs.bokeh.org/)

---

## Acknowledgements

This project was completed as part of **Summer Analytics 2025**, under the guidance of the **Consulting and Analytics Club, IIT Guwahati**, and supported by **Pathway** for real-time data processing capabilities.

---

> Developed by: **Bhavay Khandelwal**  
> Program: B.Tech (AI & Data Science), Final-Year  
> Year: 2025  





