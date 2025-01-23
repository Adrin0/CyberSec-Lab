# DVWA Vulnerable Machine Setup


## Setup Instructions


1. Clone Repository and Navigate to ELK-GPT Folder:
   ```bash
   git clone https://github.com/adrin0/CyberSec-Lab
   cd CyberSec-Lab/DVWA

2. Run Setup Script:
    ```bash 
    chmod +x setup.sh
    ./setup.sh

3. Update DVWA config file:
    ```bash
    cd DVWA/config
    sudo cp config.inc.php.dist config.inc.php
    sudo nano config.inc.php
    
- Update the database username and password settings:
    ```php
    $_DVWA[ 'db_user' ] = 'root';
    $_DVWA[ 'db_password' ] = 'your_mysql_root_password';

4. Install and Configure MySQL:
- Follow the prompts to set a root password and secure your MySQL installation.     
    ```bash
    sudo mysql_secure_installation

- Log into MySQL, Create a user, and grant it priveleges:
    ```bash
    sudo mysql -u root -p
    CREATE USER '<username>'@'localhost' IDENTIFIED BY '<password>';
    GRANT ALL PRIVILEGES ON dvwa.* TO 'adrino'@'localhost';
    FLUSH PRIVILEGES;
    EXIT;

5. Enable Apache Modules:
    ```bash
    sudo a2enmod rewrite
    sudo systemctl restart apache2

6. Finalize DVWA setup in Browser:
- Open your web browser and go to `http://<DVWA_ip>/DVWA/setup.php.`

7. Configure etc/filebeat/filebeat.yml, /etc/metricbeat/metricbeat.yml, etc/packetbeat/packetbeat.yml to send beats to Elasticsearch:

- Scroll to line #1106 and replace the IP address with the IP address of your ELK machine.

  ```yaml
  output.elasticsearch:
  hosts: ["<ELK_IP>:9201"]
  username: "adrino"
  password: "adrino"
  ```

- Scroll to line #1806 and replace the IP address with the IP address of your ELK machine.

  ```yaml   
  setup.kibana:
  host: "<ELK_IP>:5602"
  ```
- Change `xpack-monitoring` to `true`

- enable elastocsearch-xpack module for filebeat and metricbeat
    ```bash
    sudo metricbeat modules enable elasticsearch-xpack
    sudo filebeat modules enable elasticsearch-xpack

- Setup dashboards in Kibana:
    ```bash
    sudo filebeat setup --dashboards
    sudo packetbeat setup --dashboards
    sudo metricbeat setup --dashboards

