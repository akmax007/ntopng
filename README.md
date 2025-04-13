## 🛡️ Home Network SIEM with ntopng
This project documents the setup of a lightweight Security Information and Event Management (SIEM) system for monitoring a home network using ntopng.

## 📌 Overview
The goal is to have visibility into all inbound and outbound traffic on the home network, detect anomalies, and maintain a simple yet effective monitoring solution without the overhead of a full enterprise SIEM.

## 🔧 Tools Used
    ntopng: Network traffic visibility and analysis.

    nProbe (optional): For enhanced NetFlow/sFlow/IPFIX collection.

    Redis: ntopng dependency.

    pfSense/OpenWrt: (Optional) for routing and mirroring traffic to ntopng.

    Docker: (Optional) for containerized deployment.

    InfluxDB + Grafana: (Optional) for historical metrics and dashboards.

## ⚙️ Architecture

    [ Devices ] ---> [ Router (Port Mirroring) ] ---> [ ntopng ]
                                                    
                      OR

    [ Devices ] ---> [ SPAN Port / TAP ] ---> [ ntopng ]
Monitored devices include PCs, smartphones, IoT, etc.

Traffic is mirrored or routed to the ntopng instance for inspection.

## 🚀 Setup
1. Install ntopng

# Ubuntu/Debian-based
    sudo apt update
    sudo apt install ntopng
Or via Docker:

    docker run --net=host \
    -v /etc/ntopng:/etc/ntopng \
    -v /var/lib/ntopng:/var/lib/ntopng \
    ntop/ntopng
2. Configuration:
    Edit /etc/ntopng/ntopng.conf:
    -G=/var/run/ntopng.pid
    -i=eth0            # Interface to monitor
    --community        # Free license mode
    --local-networks="192.168.1.0/24"
   
4. Access Web UI
Once running, access ntopng via:

       http://<your-ip>:3000
Default credentials:

    User: admin
    Pass: admin

## 🔍 Features Enabled
  
  Real-time traffic analysis
  GeoIP resolution
  Top talkers and flows
  DNS and protocol breakdowns
  Alerting based on heuristics (e.g., DoS, data exfiltration patterns)
  Export to JSON or syslog for SIEM integration

## 📊 Sample Dashboards

    ![excitel](https://github.com/user-attachments/assets/f7f0946a-e5d4-4f70-95cf-af6faef25f4b)
    ![europe](https://github.com/user-attachments/assets/778fb4d3-7b52-4340-a67a-7da0aceb2a57)
    ![5](https://github.com/user-attachments/assets/4b8a730d-2872-46cf-80fb-1a7361ae99b1)
    ![4](https://github.com/user-attachments/assets/cc5523a7-778e-484b-a5a7-c2209d548a29)
    ![3](https://github.com/user-attachments/assets/e86a8220-0d94-4aa7-b99d-dce25b6f4769)
    ![2](https://github.com/user-attachments/assets/29e421c4-2250-4cd8-b692-5aabce4dcafc)
    ![google](https://github.com/user-attachments/assets/795125a6-c031-4699-a480-c38ee07b749c)


## 💡 Future Plans
    ✅ Basic traffic visibility
    ⬜ Integrate with Suricata for IDS/IPS
    ⬜ Export to ELK or Loki/Grafana stack
    ⬜ Anomaly detection via custom scripts or ML
