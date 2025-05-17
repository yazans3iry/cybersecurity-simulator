# Interactive Cybersecurity Training Simulator for Attack Detection and Response

A comprehensive educational environment that simulates real cyberattacks, monitors network traffic, detects threats, and guides users on appropriate response actions.

## Table of Contents

1. [Project Overview](#project-overview)
2. [System Architecture](#system-architecture)
3. [Installation Guide](#installation-guide)
4. [Virtual Machine Setup](#virtual-machine-setup)
5. [Attack Scenarios](#attack-scenarios)
6. [Traffic Monitoring Configuration](#traffic-monitoring-configuration)
7. [AI Model for Attack Detection](#ai-model-for-attack-detection)
8. [User Interface Guide](#user-interface-guide)
9. [Testing and Demonstration](#testing-and-demonstration)
10. [Presentation Guide](#presentation-guide)
11. [Future Enhancements](#future-enhancements)
12. [Troubleshooting](#troubleshooting)
13. [References](#references)

## Project Overview

The Interactive Cybersecurity Training Simulator is designed to provide hands-on experience in detecting and responding to real-world cyberattacks. This project combines virtualization technology, network traffic analysis, machine learning, and an interactive user interface to create an immersive learning environment for cybersecurity students and professionals.

### Key Features

- **Realistic Attack Simulation**: Multiple attack scenarios including port scanning, brute force, web attacks, data exfiltration, and backdoor installation
- **Real-time Traffic Monitoring**: Integration with professional tools like Zeek, Wireshark, and Suricata
- **AI-based Attack Detection**: Machine learning model that analyzes traffic patterns to identify potential threats
- **Interactive User Interface**: Dashboard displaying network status, alerts, and educational guidance
- **Educational Guidance**: Step-by-step instructions on how to respond to detected attacks
- **Modular Architecture**: Easily extensible with new attack scenarios and detection methods

### Target Audience

This simulator is designed for:
- Cybersecurity students seeking hands-on experience
- Security professionals practicing incident response
- Educational institutions teaching network security courses
- Organizations conducting security awareness training

## System Architecture

The system consists of three main environments connected through a virtualized network:

1. **Attacker Environment**: Kali Linux VM with penetration testing tools
2. **Target Environment**: Ubuntu Server VM with intentionally vulnerable services
3. **Monitoring Environment**: Security monitoring VM with traffic analysis tools and AI detection

![System Architecture](/home/ubuntu/cybersecurity_simulator/architecture/system_architecture.png)

For detailed information about the system architecture, refer to the [architecture documentation](/home/ubuntu/cybersecurity_simulator/architecture/system_architecture.dot).

## Installation Guide

### Prerequisites

- **Hardware Requirements**:
  - CPU: Quad-core processor (Intel i5/i7 or AMD Ryzen 5/7)
  - RAM: Minimum 16GB (32GB recommended)
  - Storage: 100GB free space (SSD recommended)
  - Network: Ethernet adapter with promiscuous mode support

- **Software Requirements**:
  - VirtualBox 6.1+ or VMware Workstation 16+
  - Python 3.8+
  - Git

### Installation Steps

1. **Clone the Repository**

```bash
git clone https://github.com/yourusername/cybersecurity-simulator.git
cd cybersecurity-simulator
```

2. **Install Dependencies**

```bash
pip install -r requirements.txt
```

3. **Import Virtual Machines**

Import the provided OVA files into VirtualBox or VMware:
- `attacker-kali.ova` (Attacker Environment)
- `target-ubuntu.ova` (Target Environment)
- `monitoring-ubuntu.ova` (Monitoring Environment)

4. **Configure Network**

Set up a host-only network in your virtualization software:
- Network Name: `vboxnet0` or similar
- Network CIDR: `192.168.100.0/24`
- DHCP: Disabled

5. **Start Virtual Machines**

Start the VMs in the following order:
1. Target Environment
2. Monitoring Environment
3. Attacker Environment

6. **Verify Connectivity**

From the Monitoring Environment, verify connectivity to both the Target and Attacker VMs:
```bash
ping 192.168.100.20  # Target VM
ping 192.168.100.200  # Attacker VM
```

7. **Start the Simulator Interface**

From the Monitoring Environment, start the simulator interface:
```bash
cd /opt/cybersecurity-simulator
python3 ui/cybersecurity_simulator_ui.py
```

Access the web interface at `http://localhost:8501`

## Virtual Machine Setup

Detailed specifications for each virtual machine are provided below. For complete setup instructions, refer to the [VM specifications document](/home/ubuntu/cybersecurity_simulator/vm_specs/vm_specifications.md).

### Attacker Environment (Kali Linux)

- **Base OS**: Kali Linux 2023.1
- **IP Address**: 192.168.100.200
- **Username**: kali
- **Password**: kali
- **Installed Tools**:
  - Metasploit Framework
  - Nmap
  - Hydra
  - Burp Suite
  - SQLmap
  - Wireshark

### Target Environment (Ubuntu Server)

- **Base OS**: Ubuntu Server 22.04 LTS
- **IP Address**: 192.168.100.20
- **Username**: ubuntu
- **Password**: vulnerable
- **Vulnerable Services**:
  - OpenSSH Server (with weak configuration)
  - Apache Web Server (with vulnerable web application)
  - MySQL Database (with weak credentials)
  - FTP Server (with anonymous access)

### Monitoring Environment (Ubuntu Desktop)

- **Base OS**: Ubuntu Desktop 22.04 LTS
- **IP Address**: 192.168.100.100
- **Username**: analyst
- **Password**: secure
- **Installed Tools**:
  - Zeek Network Security Monitor
  - Wireshark/TShark
  - Suricata IDS
  - ELK Stack (Elasticsearch, Logstash, Kibana)
  - Python 3.10 with data science packages
  - Cybersecurity Simulator UI

## Attack Scenarios

The simulator includes multiple attack scenarios that represent common real-world threats. For detailed information about each scenario, refer to the [attack scenarios document](/home/ubuntu/cybersecurity_simulator/attack_scenarios/attack_scenarios.md).

### Available Scenarios

1. **Reconnaissance and Port Scanning**
   - Attacker identifies open ports and services on the target
   - Uses tools like Nmap for service enumeration
   - Detection based on connection patterns and port entropy

2. **Brute Force Authentication**
   - Attacker attempts to guess credentials for SSH or web login
   - Uses tools like Hydra for automated password guessing
   - Detection based on failed login attempts and connection patterns

3. **Web Application Exploitation**
   - Attacker exploits vulnerabilities in web applications
   - Includes SQL injection, XSS, and file inclusion attacks
   - Detection based on HTTP request patterns and error responses

4. **Privilege Escalation**
   - Attacker gains higher privileges after initial access
   - Exploits misconfigured permissions or vulnerable software
   - Detection based on unusual process activity and file access

5. **Data Exfiltration**
   - Attacker extracts sensitive data from the target
   - Uses various channels for data transfer
   - Detection based on unusual data volumes and destination patterns

6. **Backdoor Installation**
   - Attacker establishes persistent access to the target
   - Creates hidden services or scheduled tasks
   - Detection based on unexpected connections and timing patterns

7. **Lateral Movement**
   - Attacker moves through the network to access additional systems
   - Uses techniques like pass-the-hash or remote execution
   - Detection based on unusual authentication patterns

### Running Attack Scenarios

Each attack scenario can be executed from the Attacker VM using provided scripts:

```bash
# From the Attacker VM
cd /opt/attack-scenarios
./run_scenario.sh port_scan
```

Available scenario options:
- `port_scan`
- `brute_force`
- `web_attack`
- `privilege_escalation`
- `data_exfiltration`
- `backdoor`
- `lateral_movement`

## Traffic Monitoring Configuration

The monitoring environment is configured with multiple tools for comprehensive traffic analysis. For detailed configuration information, refer to the [traffic monitoring document](/home/ubuntu/cybersecurity_simulator/monitoring_tools/traffic_monitoring_tools.md).

### Zeek Network Security Monitor

Zeek provides deep packet inspection and event-based analysis:

- **Configuration Files**: Located in `/opt/zeek/etc`
- **Custom Scripts**: Located in `/opt/zeek/share/zeek/site`
- **Log Files**: Located in `/opt/zeek/logs`

Key Zeek logs:
- `conn.log`: Connection metadata
- `http.log`: HTTP requests and responses
- `dns.log`: DNS queries and responses
- `ssl.log`: SSL/TLS handshakes
- `notice.log`: Security notices and alerts

### Wireshark/TShark

Wireshark provides packet-level capture and analysis:

- **Capture Interface**: `eth0` (monitoring interface)
- **Capture Filters**: Configured for relevant protocols
- **Display Filters**: Preset filters for attack detection
- **Automated Capture**: TShark scripts for continuous monitoring

### Suricata IDS

Suricata provides rule-based intrusion detection:

- **Configuration File**: `/etc/suricata/suricata.yaml`
- **Rule Files**: Located in `/etc/suricata/rules`
- **Custom Rules**: Located in `/etc/suricata/rules/custom.rules`
- **Log Files**: Located in `/var/log/suricata`

### ELK Stack

The ELK Stack provides log aggregation and visualization:

- **Elasticsearch**: Stores and indexes log data
- **Logstash**: Processes and normalizes logs from multiple sources
- **Kibana**: Provides visualization and dashboard interface
- **Filebeat**: Collects and forwards log files

### Starting Monitoring Services

All monitoring services can be started using the provided script:

```bash
# From the Monitoring VM
sudo /opt/cybersecurity-simulator/scripts/start_monitoring.sh
```

Individual services can be started separately:

```bash
# Start Zeek
sudo systemctl start zeek

# Start Suricata
sudo systemctl start suricata

# Start ELK Stack
sudo systemctl start elasticsearch
sudo systemctl start logstash
sudo systemctl start kibana
```

## AI Model for Attack Detection

The simulator includes a machine learning model for detecting various types of attacks. For detailed information about the model, refer to the [AI model document](/home/ubuntu/cybersecurity_simulator/ai_model/ai_model.md) and the [model training explanation](/home/ubuntu/cybersecurity_simulator/ai_model/model_training_explanation.md).

### Model Overview

- **Algorithm**: Random Forest Classifier
- **Features**: 20+ network traffic characteristics
- **Attack Types**: Port scanning, brute force, web attacks, data exfiltration, backdoor
- **Accuracy**: ~95% on test dataset
- **Implementation**: Python with scikit-learn

### Feature Engineering

The model uses features extracted from network traffic, including:

- Connection counts and rates
- Bytes transferred and packet sizes
- Protocol distribution
- Port and IP entropy
- Connection state distribution
- Service-specific metrics

### Model Training

The model is trained on a dataset of normal and attack traffic:

- **Training Data**: 80% of available samples
- **Testing Data**: 20% of available samples
- **Cross-Validation**: 5-fold cross-validation
- **Hyperparameter Tuning**: Grid search for optimal parameters

### Real-time Detection

The trained model is used for real-time attack detection:

1. Network traffic is captured and processed in time windows
2. Features are extracted from the processed traffic
3. The model classifies each sample as normal or a specific attack type
4. Detection results are displayed in the user interface
5. Confidence scores indicate the model's certainty

### Running the Detection System

The detection system can be started using the provided script:

```bash
# From the Monitoring VM
cd /opt/cybersecurity-simulator
python3 ai_model/detection_system.py
```

## User Interface Guide

The simulator includes an interactive user interface for monitoring, detection, and response. For detailed information about the UI, refer to the [UI implementation](/home/ubuntu/cybersecurity_simulator/ui/cybersecurity_simulator_ui.py).

### Dashboard Overview

The main dashboard provides a comprehensive view of the network status:

- **Traffic Overview**: Real-time visualization of network traffic
- **Alert Panel**: Displays detected attacks and security events
- **System Status**: Shows the status of monitoring services
- **Attack Timeline**: Chronological view of security events

### Traffic Visualization

The traffic visualization panel shows:

- **Connection Graph**: Visual representation of network connections
- **Protocol Distribution**: Breakdown of traffic by protocol
- **Traffic Volume**: Time-series chart of traffic volume
- **Port Activity**: Heatmap of active ports

### Alert System

The alert system provides:

- **Real-time Alerts**: Notifications of detected attacks
- **Severity Levels**: Color-coded severity indicators
- **Attack Details**: Detailed information about each alert
- **False Positive Handling**: Options to mark false positives

### Educational Guidance

The educational guidance system provides:

- **Attack Explanations**: Detailed descriptions of detected attacks
- **Learning Resources**: Links to educational materials
- **Step-by-Step Guidance**: Instructions for investigating alerts
- **Quiz Mode**: Interactive questions to test knowledge

### Response Recommendations

The response recommendations panel provides:

- **Immediate Actions**: Steps to contain the threat
- **Investigation Steps**: How to gather more information
- **Mitigation Strategies**: Long-term solutions to prevent recurrence
- **Command References**: Useful commands for response actions

### Starting the User Interface

The user interface can be started using the provided script:

```bash
# From the Monitoring VM
cd /opt/cybersecurity-simulator
python3 ui/cybersecurity_simulator_ui.py
```

Access the web interface at `http://localhost:8501`

## Testing and Demonstration

The simulator includes example datasets and simulated attack sessions for testing and demonstration. For detailed information, refer to the [example datasets](/home/ubuntu/cybersecurity_simulator/example_datasets) directory.

### Example Datasets

The following datasets are provided:

- `combined_dataset.csv`: Complete dataset with all traffic samples
- `training_dataset.csv`: Dataset for training the model
- `testing_dataset.csv`: Dataset for testing the model
- Attack-specific datasets for each attack type

### Simulated Attack Sessions

Detailed simulated attack sessions are provided in `attack_sessions.json`, including:

- Step-by-step attack execution
- Expected outputs and observations
- Feature vectors at each step
- Detection indicators
- Response recommendations

### PCAP Files

Packet capture (PCAP) files are described in `pcap_descriptions.json`, including:

- File details and contents
- Notable features for analysis
- Wireshark filters for examination
- Usage instructions

### Running Demonstrations

To run a demonstration using the provided datasets:

```bash
# From the Monitoring VM
cd /opt/cybersecurity-simulator/example_datasets
python3 run_demonstration.py --scenario port_scan
```

Available demonstration scenarios:
- `port_scan`
- `brute_force`
- `web_attack`
- `data_exfiltration`
- `backdoor`

## Presentation Guide

A comprehensive presentation strategy is provided to help you present this project to your graduation committee. For detailed information, refer to the [presentation strategy document](/home/ubuntu/cybersecurity_simulator/presentation/presentation_strategy.md).

### Presentation Structure

The recommended presentation structure includes:

1. **Introduction**: Problem statement and project vision
2. **System Architecture**: Overview of components and interactions
3. **Attack Scenarios**: Demonstration of selected attacks
4. **Detection System**: Explanation of the AI-based detection
5. **User Interface**: Walkthrough of the interactive interface
6. *
(Content truncated due to size limit. Use line ranges to read in chunks)
