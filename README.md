## Security Monitoring Homelab

**Author**: Christian Garces  
**Lab Focus**: Building an end-to-end security monitoring pipeline using Wazuh SIEM and Suricata IDS.

---

### Overview

This project documents the deployment of a small-scale **Security Information and Event Management (SIEM)** environment using **Wazuh** and **Suricata**. The objective of the lab was to:

- **Collect** host telemetry from an endpoint  
- **Inspect** network traffic with an IDS sensor  
- **Generate** intrusion alerts  
- **Ingest & correlate** events in a centralized SIEM  
- **Visualize & investigate** detections in a dashboard  

The lab consists of a Wazuh server running on an Ubuntu virtual machine and a Raspberry Pi endpoint running both the Wazuh agent and Suricata IDS. The Raspberry Pi acts as the network intrusion detection sensor while forwarding structured alerts to the Wazuh SIEM for analysis and visualization.

---

### Lab Architecture

- **SIEM Platform**: `Wazuh` (Manager, Indexer, Dashboard) on `Ubuntu Server`  
- **IDS Sensor / Endpoint**: `Raspberry Pi` running `Suricata` and `Wazuh Agent`  
- **Network**: Home lab network with Raspberry Pi monitoring traffic on its primary interface  

**Logical architecture:**

```text
        Home / Lab Network
                 │
         +-------+--------+
         |   Raspberry Pi |
         |  Suricata IDS  |
         |  Wazuh Agent   |
         +-------+--------+
                 │  Suricata JSON Alerts (eve.json)
                 ▼
        +---------------------+
        |  Ubuntu Server VM   |
        |  Wazuh Manager      |
        |  Wazuh Indexer      |
        |  Wazuh Dashboard    |
        +---------------------+
```

*Figure 1 – High-level architecture: Suricata on Raspberry Pi generates alerts that are forwarded to the Wazuh SIEM stack on Ubuntu.*

---

### Environment Setup

#### Wazuh SIEM Deployment (Ubuntu Server)

The first step was deploying the Wazuh SIEM stack on an Ubuntu Server VM. The stack includes three primary components:

- **Wazuh Manager** – collects and analyzes security events  
- **Wazuh Indexer** – stores and indexes event data  
- **Wazuh Dashboard** – provides the web interface for security monitoring  

<img width="872" height="523" alt="image" src="https://github.com/user-attachments/assets/954ce37c-f96b-4995-a04a-13ee25c18cd3" />

*Figure 2 – Wazuh server, dashboard, and indexer successfully installed on Ubuntu Server.*

After installation, the Wazuh dashboard was accessed from the host machine to confirm that the SIEM platform was operational.

<img width="1919" height="923" alt="image" src="https://github.com/user-attachments/assets/6f305261-6007-4add-ac08-f415ac5c9eb4" />

*Figure 3 – Wazuh dashboard login and initial view from the host OS.*

---

#### Endpoint Agent Enrollment (Raspberry Pi)

To collect host telemetry, a **Wazuh agent** was installed on a Raspberry Pi endpoint.

<img width="822" height="327" alt="image" src="https://github.com/user-attachments/assets/775a2998-1a2a-48d1-82f4-d5c3b41af447" />

*Figure 4 – Wazuh agent installed and configured on the Raspberry Pi.*

The Ubuntu server’s IP address was identified so that the agent could communicate with the Wazuh manager.

<img width="583" height="150" alt="image" src="https://github.com/user-attachments/assets/9d1c253b-d169-4764-9bf6-b28dba61b47f" />

*Figure 5 – Wazuh server IP address used by the Raspberry Pi agent for enrollment.*

---

### Suricata IDS Deployment & Configuration

#### Installing Suricata

Suricata was installed on the Raspberry Pi to act as a **network intrusion detection sensor**.

<img width="1563" height="510" alt="image" src="https://github.com/user-attachments/assets/e2788212-7e41-4ab0-981f-e350bb4aa293" />

*Figure 6 – Suricata successfully installed on the Raspberry Pi.*

The IDS service was confirmed running.

<img width="1066" height="219" alt="image" src="https://github.com/user-attachments/assets/1a4e6486-700b-43be-91ae-c62fd95482de" />

*Figure 7 – Suricata service running and enabled.*

Next, the system interfaces were inspected to determine which network interface Suricata should monitor.

<img width="687" height="225" alt="image" src="https://github.com/user-attachments/assets/2ea2c530-0ed6-4175-89ca-758569fb06bc" />

*Figure 8 – Network interfaces on the Raspberry Pi used to select the monitored interface.*

#### Suricata Configuration

The Suricata installation directory contains configuration files, rule sets, and runtime logs.

<img width="687" height="225" alt="image" src="https://github.com/user-attachments/assets/863a5eca-7239-4065-8797-b92d5db8604b" />

*Figure 9 – Suricata directory structure containing configuration files and rule sets.*

Suricata includes a number of default detection rules.

<img width="1383" height="980" alt="image" src="https://github.com/user-attachments/assets/c666da08-ec44-4146-8f8d-69f02dff8c60" /> <img width="1304" height="614" alt="image" src="https://github.com/user-attachments/assets/20550159-452f-470f-a55c-2e2024419702" />

*Figure 10 – Rules that come prepackaged with Suricata.*

The main configuration file `suricata.yaml` was edited to match the lab network environment.

**Changes made:**

- Updated `HOME_NET` to match the monitored subnet `192.168.122.0/24`  
- Updated `af-packet` interface to the correct network interface  

<img width="1919" height="962" alt="image" src="https://github.com/user-attachments/assets/64c67b3e-c89e-4e98-9986-1174868538cd" />

*Figure 11 – `suricata.yaml` tuned for the lab network (HOME_NET and af-packet interface).*

Suricata rule paths were also confirmed within the configuration.

<img width="1919" height="844" alt="image" src="https://github.com/user-attachments/assets/27c89a2c-8cab-486f-8b5c-8a53cad07408" />

*Figure 12 – Suricata rule path configuration and enabled rule files.*

#### Installing Emerging Threats Rule Sets

To enable network attack detection, the **Emerging Threats** community rule set was installed.

<img width="1919" height="805" alt="image" src="https://github.com/user-attachments/assets/b0b363da-0170-4d20-924e-b664291e1f10" />

*Figure 13 – Installing Emerging Threats rule sets for Suricata.*

Additional rule sources available for Suricata were also reviewed and installed.

<img width="909" height="216" alt="image" src="https://github.com/user-attachments/assets/295cc442-c451-4926-bf93-6ebbc5aeab16" />
<img width="1919" height="392" alt="image" src="https://github.com/user-attachments/assets/79b16e3f-8788-424f-8557-2994b116bb04" />

*Figure 14 – Managing and updating additional Suricata rule sources.*

Suricata configuration was then validated.

<img width="1071" height="282" alt="image" src="https://github.com/user-attachments/assets/017997f9-f24e-48c9-bcb0-9f8605e71cff" />

*Figure 15 – Validation confirming Suricata successfully loaded the Emerging Threats rule set.*

---

### Suricata Logging & Telemetry

Suricata generates several log files that capture different types of telemetry.

<img width="1760" height="316" alt="image" src="https://github.com/user-attachments/assets/05178bfc-358f-4779-9e5f-61dbf7d7c821" />

*Figure 16 – Suricata log directory with multiple telemetry files.*

**Key log files include:**

- `eve.json` – structured JSON event logs used for SIEM ingestion  
- `fast.log` – quick human-readable alerts  
- `stats.log` – Suricata performance statistics  
- `suricata.log` – Suricata runtime messages and diagnostics  

---

### Monitoring & Detection Workflow

#### Validating IDS Detection

Suricata runtime logs were reviewed to confirm successful initialization.

<img width="1604" height="166" alt="image" src="https://github.com/user-attachments/assets/96696a68-6055-49fd-9f9a-552864c25d01" />

*Figure 17 – Suricata startup logs confirming the IDS engine is active.*

Test network traffic was generated to trigger IDS detections, verifying that the rule set successfully identified potentially malicious activity.

<img width="1270" height="291" alt="image" src="https://github.com/user-attachments/assets/e19ba46f-4ece-4110-870a-e6e25bf633f7" />

*Figure 18 – Suricata detection generated by test IDS traffic.*

Custom Suricata detection rules were implemented to detect ICMP, SSH, and HTTP traffic directed toward the monitored network.

<img width="1919" height="976" alt="image" src="https://github.com/user-attachments/assets/89f55483-442f-4dd7-9771-3be532dc6841" />
<img width="1361" height="333" alt="image" src="https://github.com/user-attachments/assets/2d68bd5d-7cdc-46b9-9903-bb1ca92535ae" />

*Figure 19 – Custom Suricata rules and configuration loading both community and custom rule sets.*

Configuration validation confirmed the IDS engine successfully loaded all rules.

<img width="1919" height="480" alt="image" src="https://github.com/user-attachments/assets/e7f52186-2d8d-4ece-979f-d45668c2935c" />

*Figure 20 – Validation output confirming active custom and community rules.*

---

#### Real-Time IDS Monitoring

Suricata alerts were monitored using the `fast.log` file.

<img width="652" height="241" alt="image" src="https://github.com/user-attachments/assets/ae075191-ec86-4211-840d-1945b3199df0" />

*Figure 21 – Suricata detecting multiple network events in real time as test traffic is generated.*

While monitoring the Suricata alert log using:

```bash
tail -f /var/log/suricata/fast.log
```

test traffic such as ICMP pings and SSH connection attempts was generated from another terminal. As packets traversed the monitored interface, Suricata inspected them against its loaded detection signatures and immediately generated alerts when matching activity was detected.

---

### Parsing Suricata JSON Logs

Suricata’s `eve.json` output contains structured event data but is difficult to read directly.

<img width="1915" height="1037" alt="image" src="https://github.com/user-attachments/assets/3d18f918-a781-4ec3-afc5-8cf4d9b0e929" />

*Figure 22 – Raw `eve.json` output from Suricata.*

The `jq` utility was used to filter and parse JSON alerts.

<img width="930" height="245" src="https://github.com/user-attachments/assets/caf96f09-c83a-4867-9b8c-f16554e2955b" /> <img width="1249" height="641" src="https://github.com/user-attachments/assets/4446bf88-8f18-498c-a4d3-1fcd989a688f" />

*Figure 23 – Using `jq` to parse Suricata JSON alerts for easier analysis.*

**Command used:**

```bash
sudo tail -f /var/log/suricata/eve.json | jq 'select(.event_type=="alert")'
```

This command streams the Suricata event log in real time and filters only IDS alert events.

---

### Integrating Suricata with Wazuh

To centralize IDS alerts, Wazuh was configured to ingest Suricata event logs.

<img width="1919" height="956" src="https://github.com/user-attachments/assets/33f244dd-cbda-4bae-8a1e-8f3a73b39c48" />

*Figure 24 – Wazuh configuration monitoring the Suricata `eve.json` log via a `<localfile>` entry.*

A `<localfile>` entry was added to `ossec.conf` instructing Wazuh to monitor the Suricata `eve.json` log, allowing Suricata alerts to be forwarded directly into the Wazuh SIEM.

---

### Visualizing IDS Alerts in the SIEM

After integration, Suricata alerts became visible within the Wazuh dashboard.

<img width="1919" height="920" src="https://github.com/user-attachments/assets/175371e3-835a-48e9-aac8-9540c000512e" /> <img width="1094" height="803" src="https://github.com/user-attachments/assets/6b48ecdf-3ac6-4d91-9da5-ee66f2026d53" />

*Figure 25 – Suricata alerts ingested into Wazuh and visualized via the Discover dashboard.*

The Discover dashboard was used to filter events. Filtering by:

```text
rule.groups:suricata
```

isolates IDS alerts from other system logs such as PAM authentication events.

---

### Attack Simulation Testing

Multiple simulated attacks were performed to validate detection.

**Example brute-force SSH activity:**

```bash
for i in {1..30}; do
  ssh fakeuser@192.168.122.25
done
```

These actions generated Suricata alerts that were successfully ingested by Wazuh and visualized in the SIEM dashboard, confirming end-to-end visibility from network events to SIEM.

---

### Result & Learning Outcomes

This lab successfully demonstrated an end-to-end security monitoring pipeline:

```text
Network Traffic
        ↓
Suricata IDS Sensor (Raspberry Pi)
        ↓
Structured JSON Alerts (eve.json)
        ↓
Wazuh SIEM Ingestion
        ↓
Centralized Security Event Analysis
```

The project showcases hands-on experience with:

- Intrusion detection systems (IDS) deployment and configuration  
- SIEM integration and log forwarding  
- Detection rule creation and management (community and custom rules)  
- Log parsing and enrichment using tools like `jq`  
- Security event visualization and investigation in a SIEM dashboard  

This structured homelab closely mirrors real-world security operations workflows by combining network IDS telemetry with centralized, queryable security analytics.

