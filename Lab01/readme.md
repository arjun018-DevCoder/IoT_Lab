# Lab 01: Hosting an IoT Dashboard with Nginx on AWS

### Objectives
- Access the AWS Console through the sandbox environment
- Launch an AWS EC2 instance
- Configure security groups for IoT data access
- Install and configure Nginx web server
- Deploy a sample IoT dashboard web page
- Verify accessibility of the hosted dashboard via browser

### Background Theory

Cloud Computing in IoT Systems
Cloud platforms are critical for IoT deployments because they provide:

- Scalability: Handle fluctuating device connections and data streams.
- Data Aggregation: Collect sensor data centrally for analysis.
- Remote Accessibility: Allow users to monitor IoT devices from anywhere.
- Cost Efficiency: Pay-as-you-go pricing avoids heavy upfront infrastructure costs.
- Security: Protect IoT data with encryption, IAM roles, and firewalls

###  AWS EC2 (Elastic Compute Cloud)
AWS EC2 provides virtual servers for hosting applications. Key features:  
- **Elastic Scaling**: Adjust compute resources dynamically  
- **Security Groups**: Control inbound/outbound traffic  
- **AMI Flexibility**: Choose OS images tailored for web hosting  
- **Global Infrastructure**: Deploy dashboards close to IoT devices for low latency  

###  Nginx Web Server
Nginx is a lightweight, high-performance web server. Benefits:  
- **Efficient Handling**: Manages multiple IoT data requests simultaneously  
- **Low Resource Usage**: Ideal for small EC2 instances  
- **Reliability**: Stable for long-running IoT dashboards  
- **Flexibility**: Serves static dashboards and proxies IoT APIs  
- **Simple Configuration**: Easy to set up and customize  

---

## Procedure

### Step 1: Access AWS Console
- Log in to AWS Management Console  
- Navigate to **EC2 Dashboard**  
- Verify region (e.g., `us-east-1`)  

### Step 2: Launch EC2 Instance
- **AMI**: Select Ubuntu Server 22.04 LTS  
- **Instance Type**: t2.micro (free tier)  
- **Storage**: Default 30GB gp2 volume  
- **Tags**: Name → IoT-Dashboard 
- **Security Group**:  
  - HTTP (Port 80) → 0.0.0.0/0  
  - SSH (Port 22) → Your IP  
- Launch and download key pair  

### Step 3: Connect & Install Nginx
```bash
ssh -i "your-key.pem" ubuntu@your-public-ip
sudo apt update
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx

Nginx Installation for lightweight IoT dashboards

Dashboard Hosting accessible via public IP

Cloud Benefits: scalability, remote monitoring, and cost efficiency
```
### Step 4: Service Verification (Continued)
Confirm that the Nginx service is active and running properly on the system:
```bash
sudo systemctl status nginx
```

### Step 5: Deploying the IoT Dashboard Interface
1. Navigate to the default Nginx web document directory:
```bash
cd /var/www/html
```

2. Generate and open a new `index.html` file using the nano text editor:
```bash
sudo nano index.html
```

3. Populate the file with the following structured HTML and inline styles:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>IoT Environmental Monitor - Lab 2</title>
  <style>
    body { 
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; 
      background: #f4f7f6; 
      margin: 40px; 
      color: #333;
    }
    .dashboard-card { 
      background: #ffffff; 
      padding: 30px; 
      border-radius: 10px; 
      box-shadow: 0 4px 12px rgba(0,0,0,0.08); 
      max-width: 550px; 
      margin: auto;
    }
    h1 { color: #2c3e50; border-bottom: 2px solid #ecf0f1; padding-bottom: 10px; }
    .status-alert { color: #27ae60; font-weight: bold; }
    .metric { font-size: 1.1em; margin: 10px 0; }
    .highlight { font-weight: bold; color: #2980b9; }
  </style>
</head>
<body>
  <div class="dashboard-card">
    <h1>📊 IoT Dashboard - Lab 2</h1>
    <p class="status-alert">✓ Dashboard hosted successfully on AWS EC2</p>
    
    <h2>Telemetry Data</h2>
    <p class="metric">Temperature Sensor: <span class="highlight">25°C</span></p>
    <p class="metric">Humidity Sensor: <span class="highlight">60%</span></p>
    <p class="metric">System Clock: <span id="timestamp">Loading...</span></p>
    
    <script>
      document.getElementById('timestamp').textContent = new Date().toLocaleString();
    </script>
  </div>
</body>
</html>
```

4. Save and exit the editor (Ctrl+O, Enter, Ctrl+X), then update the file permissions to ensure it is publicly readable:
```bash
sudo chmod 644 /var/www/html/index.html
```

### Phase 5: Testing Dashboard Accessibility
1. Copy the public IPv4 address assigned to your EC2 instance from the AWS console.
2. Open a new browser tab and navigate to the server using the HTTP protocol:
```text
http://<your-public-ip>
```

---

## Experimental Observations & Results

### Virtual Machine Properties
* **Instance ID:** `i-0cc34def567hij890`
* **Instance Class:** `t2.micro`
* **Public IP Address:** `54.210.78.123`
* **Current State:** Running ✓

### Web Server Metrics
* **Service Status:** Active (Running)
* **Memory Footprint:** ~5MB
* **Listening Port:** 80 (HTTP)

### Application Verification
* **Target Endpoint:** `http://54.210.78.123/`
* **HTTP Response Code:** 200 OK
* **Operational Behavior:** The browser successfully renders the custom IoT dashboard displaying static sensor configurations and a dynamically rendering localized timestamp.

### Network Firewall Configuration
The following active rule profile was validated within the instance's Security Group:

| Traffic Type | Port | Source | Status |
| :--- | :--- | :--- | :--- |
| **HTTP** | 80 | `0.0.0.0/0` | Enabled ✓ |
| **SSH** | 22 | `Your IP` | Enabled ✓ |

---

## Conclusion
This practical laboratory exercise successfully demonstrated the lifecycle of hosting targeted applications on cloud infrastructure. Key takeaways include:
* Efficient navigation of the AWS Console to provision an Ubuntu Linux EC2 virtual instance.
* Attaching granular security rules to safely expose required application ports to external traffic.
* Implementing Nginx as a lightweight web daemon optimized for hosting resource-efficient IoT data interfaces.
* Validating global accessibility of local telemetry displays via public IP routing.
* Reinforcing fundamental cloud benefits, notably decoupled scalability, reliable remote monitoring pipelines, and operational cost reduction.

