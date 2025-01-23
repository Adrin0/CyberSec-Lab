# ELK Machine Setup

The ELK machine hosts the Elasticsearch, Logstash, and Kibana stack for centralized security monitoring.

## Components
- **Elasticsearch:** Stores and indexes logs.
- **Logstash:** Processes and enriches log data.
- **Kibana:** Visualizes data from Elasticsearch.

## Setup Instructions

1. Clone Repository and Navigate to ELK-GPT Folder:
   ```bash
   git clone https://github.com/adrin0/CyberSec-Lab
   cd CyberSec-Lab/ELK

2. Run Setup Script:
    ```bash 
    chmod +x setup.sh
    ./setup.sh

3. Configure UFW rules to deny any incoming traffic from the internet except what's allowed for your internal network and ELK setup, allow traffic from Beats agents, allow specific internal IPs (agents and Kali) to access the DVWA web service, allow outbound traffic on commonly used ports (HTTP, HTTPS, etc.), but restrict incoming NAT traffic to be safe.
   ```bash
   sudo ufw allow from 192.168.56.0/24 to any port 22  # SSH
   sudo ufw allow from 192.168.56.0/24 to any port 5044
   sudo ufw allow from 192.168.56.0/24 to any port 5045
   sudo ufw allow from 192.168.56.0/24 to any port 9600
   sudo ufw allow from 192.168.56.0/24 to any port 9601
   sudo ufw allow from 192.168.56.0/24 to any port 9200
   sudo ufw allow from 192.168.56.0/24 to any port 9201
   sudo ufw allow from 192.168.56.0/24 to any port 5601
   sudo ufw allow from 192.168.56.0/24 to any port 5602
   sudo ufw default deny incoming
   sudo ufw default allow outgoing
   sudo ufw enable