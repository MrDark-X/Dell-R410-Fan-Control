# 🌀 Dell R410 Fan Controller – Dockerized Web UI

A lightweight, Dockerized web application that monitors and controls the fan speed of a **Dell PowerEdge R410** server using **IPMI commands**. Designed with a user-friendly web interface and automatic fan logic based on CPU temperature thresholds.

---

## 🚀 Features

- ✅ Controls fan speed on Dell PowerEdge R410 using `ipmitool`
- ✅ Automatically switches between **manual** and **dynamic** fan control
- ✅ Web interface with **real-time output**
- ✅ Containerized for portability and easy deployment
- ✅ Minimal UI with clean styling and terminal-like output
- ✅ Written in **Bash**, **PHP**, **HTML/CSS**, and packaged with **Docker**

---

## 🛠️ How to Use

### 🐳 1. Clone the Repository

```bash
git clone https://github.com/MrDark-X/Dell-R410-Fan-Control.git
cd fan-control-web
```
---
### 🐋 2. Build the Docker Image
```bash
docker load -i fan-control-image.tar
```
### ▶️ 3. Run the Container
```bash
docker run -d -p 8080:80 fan-control-web
```

#### Access the app at http://localhost:8080

## 🔧 Configuration Notes
- The script connects to the iDRAC interface via ipmitool using LAN.
- Default iDRAC settings in fan.sh:
- IDRAC_IP="10.20.30.70"      //modify with your idrac ip
- IDRAC_USER="root"
- IDRAC_PASSWORD="calvin"
- Navigate to /var/www/html inside the Docker container and modify the above details in fan.sh script

## 🔍 How the Script Works
The script performs the following:
1. Reads CPU temperature from iDRAC using ipmitool
2. If CPU temp > 45°C:
- 🔁 Enables dynamic fan control mode (safety mode)
3. If CPU temp ≤ 45°C:
- 🛠️ Disables dynamic control and sets fan speed manually
4. Fan speed is set in steps based on temperature ranges, from 15% to 40%
This approach ensures:
- Energy efficiency (reducing fan noise & power use when cool)
- Hardware protection (switching back to auto control under high temp)

## 🔐 Security Recommendation
- This web interface executes system-level commands. To avoid misuse:
- Only run it in a trusted internal network
- Add basic authentication or restrict access via firewall
- Never expose **info.php** to the public without protection

## 📷 Screenshots
![Alt text](/images/ss-1.png?raw=true "Docker Container")
![Alt text](/images/ss-2.png?raw=true "Files")

## 📘 License
MIT License – do whatever you want, just don't blame me if your server lifts off 🚀

## 👨‍💻 Author
Yaswanth Surya Chalamalasetty

## 💡 Why This Is Useful
This project is especially useful for:
- Homelab & Data Center operators who want to:
- Reduce fan noise
- Extend fan lifespan
- Avoid overheating during high loads
- Sysadmins managing old Dell servers without granular thermal control via BIOS
- Anyone looking to automate thermal management on legacy Dell hardware
Instead of logging into iDRAC each time or manually running ipmitool, this solution gives you 1-click control in a beautiful interface you can run anywhere.

