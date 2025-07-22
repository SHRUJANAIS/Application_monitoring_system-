# Application_monitoring_system-
The Log Analytics Platform is designed to collect, process, and visualize log data in real-time. It leverages Grafana for visualization, Kafka for real-time log ingestion, and a relational database for storage.
<img width="797" height="409" alt="image" src="https://github.com/user-attachments/assets/4babcbd0-6fdb-444e-8179-e51c7ffa3b63" />  
## Running the Project
### Start all the containers
sudo sudo docker-compose down

sudo docker-compose up --build

### Check if all 6 docker instances are runing
sudo docker ps

### Start workload script separately:
python workload/simulate.py

### Setup Grafana: http://localhost:3000/ (Login: admin / admin)
#### Connect to mysql data source with following credentials
 <pre><code>
 Host: db:3306
 User: root
 Password: rootpass
 Database: logs</code></pre>
#### Create Grafana dashboards with respective queries
Request Count Per Endpoint:
<pre><code>SELECT endpoint, COUNT(*) as count FROM logs GROUP BY endpoint;</code></pre>
Response Time Trend:
<pre><code>SELECT timestamp as time, AVG(response_time) as avg_response FROM logs GROUP BY time ORDER BY time</code></pre>
Most Frequent Errors:
<pre><code>SELECT error_message, COUNT(*) FROM logs WHERE error_message IS NOT NULL GROUP BY error_message</code></pre>
Live Logs:
<pre><code>SELECT timestamp, endpoint, status_code, error_message FROM logs ORDER BY timestamp DESC LIMIT 100</code></pre>
## Debugging
### Access the container
Check the container ID in ‘sudo docker ps’ o/p sudo docker exec -it <container_id> bash

check process listing using command: ps -aef

### Debugging DB Container
`mariadb -u root -p <- provide password as rootpass`

SHOW DATABASES;

USE logs;

SHOW TABLES;

DESCRIBE logs;

SELECT * FROM logs;
