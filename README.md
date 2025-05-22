# CS_361_SIM
Microservice: Investment Simulation API

This microservice is part of a financial simulation tool.  It calculates investment portfolio performance from user-defined parameters.  It runs on Flask and communicates using a REST API. The implementation requires the Python packages numpy and scipy.

The packages will need to be installed with one of the following options:

**Python script/interactive Python session:**
```python
import sys
import subprocess

#Install required dependencies
required_packages = ["flask", "numpy", "scipy"]

for package in required_packages:
    subprocess.check_call([sys.executable, "-m", "pip", "install", package])

OR

#Python’s Interactive Shell:
```python
import pip
pip.main(["install", "flask", "numpy", "scipy"])


Communication Contract 
This contract defines how to interact with the microservice to ensure consistency for all teammates.

### How to Request Data
```json
To request data from the microservice, send a GET request to:
http://127.0.0.1:8001/sim
Example Request (Python)
python
import requests

url = "http://127.0.0.1:8001/sim"
params = {
    "user_stocks": 0.5,
    "user_bonds": 0.4,
    "user_cash": 0.1,
    "stock_ret": 0.08,
    "stock_std": 0.18,
    "stock_div": 0.025,
    "bond_ret": 0.035,
    "bond_std": 0.045,
    "bond_div": 0.015,
    "inflation_rate": 0.025,
    "inflation_std": 0.012,
    "user_horizon": 10,
    "sims": 100,
    "principal": 200000,
    "reinvest": False    # can be True or False
}

response = requests.get(url, params=params)

if response.status_code == 200:
    print("Simulation Results:")
    print(response.json())
else:
    print(f"Error: Received status code {response.status_code}")
    
## How to Receive Data

The microservice returns simulation results as a structured JSON response.

### **Example JSON Response**
```json
{
  "results": {
    "year_1": {
      "inflation": 0.022,
      "stocks": {
        "nominal_return_rate": 0.075,
        "nominal_returns": 15000,
        "real_return_rate": 0.051,
        "real_returns": 10200,
        "dividend_returns": 500,
        "stock_val": 115000
      }
    },
    "year_2": {
      "inflation": 0.020,
      "stocks": {
        "nominal_return_rate": 0.082,
        "nominal_returns": 17000,
        "real_return_rate": 0.060,
        "real_returns": 12000,
        "dividend_returns": 600,
        "stock_val": 132000
      }
    }
  }
}
Key Data Fields:
•	inflation: Inflation rate for the given year.
•	nominal_return_rate: The portfolio’s return before inflation.
•	real_return_rate: The return rate adjusted for inflation.
•	dividend_returns: Dividends earned over the year.
•	stock_val: The updated stock portfolio value.

![UML Diagram](Main/uml-diagram.png)


