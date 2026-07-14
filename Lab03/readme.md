# Lab 03 - Visualizing IoT Sensor Data Using Interactive Dashboards


---

# Objective

The objectives of this laboratory are:

- Retrieve stored sensor data from the REST API developed in Lab 02.
- Understand the importance of data visualization in IoT systems.
- Develop a web-based dashboard to display sensor data.
- Create real-time and historical visualizations of temperature and humidity.
- Deploy the dashboard on an AWS EC2 instance.
- Analyze sensor trends using graphical representations.

---

# Background Theory

## Data Visualization in IoT

IoT devices continuously generate sensor data such as temperature and humidity. Raw numerical values are difficult to understand directly, therefore dashboards and graphs are used to visualize the information for easier monitoring and analysis.

## REST API Architecture

The frontend dashboard communicates with the backend using REST APIs. This separation between frontend and backend improves scalability, maintainability, and flexibility.

## Dashboard Systems

A dashboard provides an interactive interface where users can monitor sensor readings in real time while also viewing historical trends.

## Data Filtering

Filtering allows users to retrieve data within a selected time period or range, making analysis more efficient.

# System Data Workflow
<img width="1024" height="559" alt="System_Data_workflow" src="https://github.com/user-attachments/assets/e74363f3-1d86-48ff-ae32-2ebb47b090c6" />


---

# Software Requirements

- Ubuntu Server (AWS EC2)
- Python 3
- FastAPI
- TinyDB
- Uvicorn
- Chart.js
- HTML
- CSS
- JavaScript

---

# Installation

## Update Ubuntu

```bash
sudo apt update && sudo apt upgrade -y
```

## Install Python

```bash
sudo apt install python3-pip python3-venv -y
```

## Create Project

```bash
mkdir iot-dashboard
cd iot-dashboard
```

## Create Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate
```

## Install Dependencies

```bash
pip install -r requirements.txt
```

---

# Project Structure

```
iot-dashboard/
│
├── main.py
├── db.json
├── requirements.txt
├── static/
│   └── index.html
└── README.md
```
# Requirement.txt
```
fastapi
uvicorn
tinydb
python-multipart
```
---

# Running the Server

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

---

# Dashboard URL

```
http://<EC2-PUBLIC-IP>:8000/dashboard
```

Example

```
http://54.175.84.178:8000/dashboard
```

---

# REST API(Backend code)
main.py
```
from datetime import datetime

from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware
from fastapi.responses import FileResponse
from fastapi.staticfiles import StaticFiles
from tinydb import TinyDB

app = FastAPI(title="IoT Dashboard API")

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_methods=["*"],
    allow_headers=["*"],
)

db = TinyDB("db.json")

app.mount("/static", StaticFiles(directory="static"), name="static")


@app.get("/")
def home():
    return {"message": "IoT Dashboard API Running"}


@app.get("/dashboard")
def dashboard():
    return FileResponse("static/index.html")


@app.post("/weather")
def add_weather(temperature: float, humidity: float):

    data = {
        "timestamp": datetime.now().strftime("%Y-%m-%d %H:%M:%S"),
        "temperature": temperature,
        "humidity": humidity,
    }

    db.insert(data)

    return {
        "status": "success",
        "data": data,
    }


@app.get("/weather")
def get_weather():
    return db.all()


```

## Create UI(Frontend Code)
create static/index.html

```
<!DOCTYPE html>
<html>

<head>

    <meta charset="UTF-8">

    <title>IoT Dashboard</title>

    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <style>

        body{
            margin:0;
            font-family:Arial;
            background:#f2f5f9;
        }

        header{
            background:#2a5298;
            color:white;
            text-align:center;
            padding:20px;
            font-size:28px;
        }

        .container{
            display:flex;
            justify-content:space-around;
            margin:20px;
        }

        .card{

            background:white;
            width:40%;
            padding:20px;

            border-radius:10px;

            box-shadow:0 0 10px rgba(0,0,0,.15);

            text-align:center;

        }

        .value{

            font-size:32px;

            margin-top:10px;

            font-weight:bold;

        }

        canvas{

            background:white;

            margin:20px;

            padding:10px;

            border-radius:10px;

        }

    </style>

</head>

<body>

<header>

IoT Sensor Monitoring Dashboard

</header>

<div class="container">

<div class="card">

<h2>Temperature</h2>

<div id="temp" class="value">

-- °C

</div>

</div>

<div class="card">

<h2>Humidity</h2>

<div id="hum" class="value">

-- %

</div>

</div>

</div>

<canvas id="chart"></canvas>

<script>

let chart;

async function loadData(){

const response = await fetch("/weather");

const data = await response.json();

if(data.length===0)
return;

const latest = data[data.length-1];

document.getElementById("temp").innerText = latest.temperature+" °C";

document.getElementById("hum").innerText = latest.humidity+" %";

const labels = data.map(item=>item.timestamp);

const temps = data.map(item=>item.temperature);

if(chart)
chart.destroy();

chart = new Chart(document.getElementById("chart"),{

type:"line",

data:{

labels:labels,

datasets:[{

label:"Temperature",

data:temps,

borderColor:"red",

fill:false

}]

}

});

}

loadData();

setInterval(loadData,5000);

</script>

</body>

</html>
```

Parameters

| Name | Type |
|------|------|
| temperature | float |
| humidity | float |

---

---

# Output

The dashboard displays

- Latest Temperature
- Latest Humidity
- Historical Temperature Graph

---

# Expected Results

- REST API successfully deployed.
- Dashboard accessible through AWS EC2.
- Sensor data stored in TinyDB.
- Temperature and humidity updated automatically.
- Historical graph generated using Chart.js.



# Conclusion

This laboratory demonstrates how IoT sensor data can be visualized using a web-based dashboard. FastAPI provides REST services while TinyDB stores sensor readings. The frontend dashboard uses Chart.js to display real-time and historical temperature data, enabling effective monitoring of IoT devices.
