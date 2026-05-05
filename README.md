# Analysis HW 7
Python workflow for pulling streamflow data for the Verde River near Camp Verde, AZ streamgage (USGS 09506000) and creating a 5-day daily average streamflow forecast based on historical data. For homework 7 of Hydrogeologic Analysis Tools II (HWRS564b).


## Setup
1. Clone the repository:
   git clone <your-repo-url>
   cd <your-repo-name>

2. (Recommended) Create a virtual environment:
   python -m venv env

   Activate it:
   - Mac/Linux:
     source env/bin/activate
   - Windows:
     env\Scripts\activate

3. Install required packages:
   pip install numpy pandas matplotlib hf_hydrodata


## HydroFrame Access
This workflow requires a HydroFrame account. An account can be created at: https://hydrogen.princeton.edu/

You will be prompted to enter:
- Your HydroFrame email
- Your HydroFrame PIN


## Running the Workflow

The full workflow is executed using the shell script:

    ./run_workflow.sh

This script:
1. (Optionally) trains a model
2. Downloads recent streamflow data
3. Generates a 5-day forecast
4. Saves a plot of the results

## User Options (run_workflow.sh)

You can modify the following variables in the shell script before running:

   FORECAST_DATE="2024-04-30"
   MODEL="recent_5day_avg" or "longterm_avg"

Other configurable options include:
- Training and testing date ranges
- AR model order
- Whether to refit the model (REFIT_MODEL)
- Whether to run validation (RUN_VALIDATION)

## Output

Forecast plots are saved to the outputs/ directory:

   outputs/forecast_plot_<model>.jpg

Example:
   outputs/forecast_plot_recent_5day_avg.jpg

## Model Descriptions

### 1. Long-Term Average (longterm_avg)

- Computes the mean streamflow over the entire training period
- Produces a constant forecast for all 5 days
- Requires training via train_model.py (creates saved_model.pkl)

Use case: baseline comparison model

### 2. Previous 5-Day Average (recent_5day_avg)

- Computes the average streamflow from the 5 days prior to the forecast date
- Produces a constant forecast based on recent observations
- Does NOT require training

Use case: simple short-term persistence model

## Workflow Summary

1. (Optional) Train model using train_model.py
2. Download recent data
3. Generate forecast using generate_forecast.py
4. Save forecast plot to outputs/


## Notes

- The recent_5day_avg model bypasses the training step
- The shell script is configured to skip training when this model is selected
- Forecasts are plotted alongside the previous 30 days of observed streamflow

## Author

Chloe Codner
HWRS564B: Hydrogeologic Analysis Tools & Methods, Homework 7
