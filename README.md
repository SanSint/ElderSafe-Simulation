Elder Safe Alert Logic – AI & IoT Simulation Project


📄 Project Overview

This project simulates environmental monitoring for elderly safety using IoT sensor data and AI-based logic.

The system analyzes temperature, humidity, and CO₂ levels to determine safe, warning, and danger conditions.

It integrates both real and simulated data (SML2010 dataset + synthetic samples) to trigger alerts for unsafe conditions.



- Features
 
Hybrid dataset (real + synthetic) integration

Rule-based alert logic for environmental risk

Visualization of alert distribution by factor

Python-based processing compatible with Google Colab

Ready for extension with ML or cloud IoT platforms



- Requirements

Library	Version	Description

Python 3.10 +	–	Core runtime

pandas	≥ 1.5	Data manipulation

matplotlib	≥ 3.7	Graphs & charts

numpy	≥ 1.24	Numerical operations

google.colab	–	Colab runtime support


Install with:
pip install pandas numpy matplotlib


- Files

ElderSafeAlertLogic.ipynb – main Colab notebook with code

NEW-DATA-1.T15.txt – input dataset (upload before running notebook)



- How to Run (on Google Colab)
 
1. Open the notebook in Google Colab

2. Upload NEW-DATA-1.T15.txt to the Colab workspace
   
3. Run each cell sequentially from top to bottom
   
4. View generated plots and alert summaries at the end
   
Methodology

Input Data: Temperature, humidity, and CO₂ from SML2010 dataset + simulated values

Processing: Apply rule-based alert logic using threshold ranges

Output: Summary table showing safe, warning, and danger percentages
