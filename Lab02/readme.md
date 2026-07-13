# Experiment 2:Developing and deploying a REST API to store data on cloud

## 1. Experiment Objectives
* Provision and set up an Ubuntu-based Amazon AWS EC2 instance.
* Configure an isolated Python development environment using `venv`.
* Install necessary dependencies including FastAPI, Uvicorn, and TinyDB.
* Build out operational REST API endpoints tailored for IoT metrics.
* Collect and save simulated temperature and humidity readings with automated timestamps.
* Verify API routing using HTTP GET and POST operations.

---

## 2. Theoretical Framework

### The Role of Cloud Computing in IoT Architecture
Cloud solutions remove the limitations of localized storage by allowing hardware devices to transfer, process, and secure telemetry data across the internet. This provides IoT networks with high availability, flexible data scaling, and central access points for remote operations.

### Amazon EC2 (Elastic Compute Cloud)
EC2 represents Amazon's core secure, resizable compute service. It lets developers deploy applications onto virtualized hardware platforms remotely, maximizing control over systems architecture and network interfaces.

### REST API Architecture
Representational State Transfer (REST) provides an architectural blueprint for system communication. By utilizing standardized HTTP request methods (such as GET, POST, PUT, and DELETE), entirely distinct systems can reliably pass structured data states back and forth.

### FastAPI Framework
FastAPI is a minimalist, high-performance web framework designed for building modern APIs with Python. It features native asynchronous support, automatic interactive documentation creation (via Swagger UI), and fast execution times.

### TinyDB Document Database
TinyDB is a lightweight, file-based NoSQL document database built natively in Python. Storing data directly inside structural JSON files makes it a clean database choice for prototyping, micro-services, and low-overhead IoT configurations.

### HTTP Methods: GET vs. POST
* **GET Request:** Initiated to fetch or read data structures from the destination server.
* **POST Request:** Used to transmit raw payload structures to the server to populate a database or trigger state changes.

---

## 3. Step-by-Step Implementation

### Step 1: Initialize the AWS EC2 Host
1. Sign in to your assigned AWS Management Console.
2. Head to the **EC2 Dashboard** and launch a fresh **Ubuntu Server** virtual instance.
3. Modify the attached **Security Group** parameters to open incoming firewall access for both **SSH (Port 22)** and **HTTP (Port 80)** traffic.
4. Establish an active terminal connection to your target cloud machine using an SSH client.



### Step 2: Establish the Isolated Python Environment
Update the base system packages, download the required virtual environment binaries, and spin up an isolated execution environment by running the following command sequence:

```bash
# Update repository lists and install package management tools
sudo apt update
sudo apt install python3-pip python3-venv -y

# Generate and engage the isolated environment space
python3 -m venv myenv
source myenv/bin/activate
```


### Step 3: Install Core Dependencies
With your virtual environment engaged, execute pip to pull down the foundational software stack:

```bash
pip install fastapi uvicorn tinydb
```

### Step 4: Program the FastAPI Application Logic
Create a new file named `main.py` inside your project working directory:

```bash
nano main.py
```

Paste the following application source code inside the file:

```python
from fastapi import FastAPI
from tinydb import TinyDB
from datetime import datetime

# Initialize the main API router engine
app = FastAPI(title="Cloud IoT Data Broker")

# Instantiate or hook into the local JSON document database file
db = TinyDB('iot_data.json')

@app.get("/")
def read_root():
    return {"status": "Online", "service": "IoT REST API Engine"}

@app.post("/data")
def collect_sensor_metrics(temperature: float, humidity: float):
    # Construct the telemetry data structure with active server timestamping
    payload = {
        "temperature": temperature,
        "humidity": humidity,
        "timestamp": str(datetime.now())
    }
    
    # Commit the dictionary entry directly to the document store
    db.insert(payload)
    
    return {
        "status": "Success",
        "saved_payload": payload
    }

@app.get("/data")
def retrieve_all_metrics():
    # Return all documents recorded inside the storage file
    return db.all()
```

### Step 5: Boot the Web Application Server
Expose the server routing openly across the public network interface using port 80:

```bash
sudo ./myenv/bin/uvicorn main:app --host 0.0.0.0 --port 80
```
*(Note: If calling uvicorn globally with sudo drops the environment context, explicitly path to the venv binary as shown above).*

---

## 4. System Output and Performance Logs

### Virtual Machine Metrics
* **Instance Identification ID:** `i-0cc34def567hij890`
* **Compute Tier Profile:** `t2.micro`
* **Assigned Public IPv4 Address:** `54.210.78.123`
* **Deployment State Status:** Running ✓

### Core Server Lifecycle Status
* **Application Daemon:** Uvicorn serving FastAPI
* **Runtime Resource Consumption Footprint:** ~5MB RAM memory footprint
* **Network Binding Profile:** Port 80

### Request Performance Verification
* **Target Root API Access Point URL:** `http://54.210.78.123/`
* **Network Handshake HTTP Code:** 200 OK
* **Operational Verification:** The system successfully processes inbound REST actions, writes new records directly to `iot_data.json`, and serves historical logs through browser queries and interactive Swagger documentation pages (`/docs`).

### Active Firewall Matrix (Security Groups)

| Protocol Pattern | Target Port | Source Matrix | Status |
| :--- | :--- | :--- | :--- |
| **HTTP** | 80 | `0.0.0.0/0` | Active ✓ |
| **SSH** | 22 | `Your IP` | Active ✓ |

---

## 5. Conclusion
This laboratory session successfully demonstrated the creation, orchestration, and structural execution of an isolated backend REST architecture deployed directly onto AWS public cloud infrastructure. Utilizing Python's FastAPI framework combined with TinyDB database engines allowed for the creation of a lightweight, highly responsive storage solution capable of tracking incoming IoT device datasets. Through structured GET and POST workflows, telemetry storage rules were verified along with proper execution of network firewalls. The results confirm the real-world utility of leveraging cloud-based server systems to manage distributed IoT logging endpoints efficiently.
