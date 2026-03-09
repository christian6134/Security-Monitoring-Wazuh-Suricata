# SIEM-WAZUH--IDS-SURICATA-

Installed Wazuh Server, Dashboard, Indexer on UBUNTU Server

<img width="872" height="523" alt="image" src="https://github.com/user-attachments/assets/954ce37c-f96b-4995-a04a-13ee25c18cd3" />

Logged into Wazuh Dashboard From Host OS (Lint Minux)

<img width="1919" height="923" alt="image" src="https://github.com/user-attachments/assets/6f305261-6007-4add-ac08-f415ac5c9eb4" />

Configured Wazuh Agent on Rasberry Pi

<img width="822" height="327" alt="image" src="https://github.com/user-attachments/assets/775a2998-1a2a-48d1-82f4-d5c3b41af447" />

Wazuh Server IP Address (Ubuntu Server)

<img width="845" height="251" alt="image" src="https://github.com/user-attachments/assets/bbccf8b1-0d5f-4d04-8543-d76d53ffad07" />

Configure Wazuh Agent (Rasberry Pi) to use Ubuntu Server as Wazuh Server

<img width="514" height="354" alt="image" src="https://github.com/user-attachments/assets/9de34b06-0b42-4fcd-84b7-de5d313c57f3" />

Enrolled Rasberry Pi as Agent on Ubuntu Server

<img width="499" height="330" alt="image" src="https://github.com/user-attachments/assets/c707353e-28bf-4d4c-a44e-4bc0baf8424f" />

Registered the Raspberry Pi endpoint with the Wazuh Manager using agent enrollment keys. This process establishes a trusted relationship between the agent and the centralized SIEM, ensuring authenticated log forwarding and preventing unauthorized agent connections.

<img width="1038" height="300" alt="image" src="https://github.com/user-attachments/assets/ddcb67aa-3a81-4e6e-8022-7916aeb9e886" />

Insert Key (Enrollment)

<img width="1292" height="434" alt="image" src="https://github.com/user-attachments/assets/9e2f32e0-a102-43ff-8018-5624cd7f4448" />

After completing port forwarding, rasberry pi is enrolled

<img width="583" height="150" alt="image" src="https://github.com/user-attachments/assets/9d1c253b-d169-4764-9bf6-b28dba61b47f" />

-------------

<img width="1563" height="510" alt="image" src="https://github.com/user-attachments/assets/e2788212-7e41-4ab0-981f-e350bb4aa293" />

suricata is installed and running


<img width="1066" height="219" alt="image" src="https://github.com/user-attachments/assets/1a4e6486-700b-43be-91ae-c62fd95482de" />

determine the interface(s) and IP address(es) on which Suricata should be inspecting network packets:


<img width="687" height="225" alt="image" src="https://github.com/user-attachments/assets/2ea2c530-0ed6-4175-89ca-758569fb06bc" />

suricata directory include rules, configs and .yaml


<img width="687" height="225" alt="image" src="https://github.com/user-attachments/assets/863a5eca-7239-4065-8797-b92d5db8604b" />

rules that come prepackaged in suricata


<img width="1383" height="980" alt="image" src="https://github.com/user-attachments/assets/c666da08-ec44-4146-8f8d-69f02dff8c60" />

<img width="1304" height="614" alt="image" src="https://github.com/user-attachments/assets/20550159-452f-470f-a55c-2e2024419702" />



suricata yaml config file
change 1 - change home net to match subnet / interface "192.168.122.0/24"

chane 2 - change af-packet interface :en1ps0


<img width="1919" height="962" alt="image" src="https://github.com/user-attachments/assets/64c67b3e-c89e-4e98-9986-1174868538cd" />

suricata rule file path and rule-files 
right now just suricata.rules

<img width="1919" height="844" alt="image" src="https://github.com/user-attachments/assets/27c89a2c-8cab-486f-8b5c-8a53cad07408" />

install suricata rule sets "emerging threats"


<img width="1919" height="805" alt="image" src="https://github.com/user-attachments/assets/b0b363da-0170-4d20-924e-b664291e1f10" />

listing other rule sources for suricata

<img width="909" height="216" alt="image" src="https://github.com/user-attachments/assets/295cc442-c451-4926-bf93-6ebbc5aeab16" />

installing extra sources


<img width="1919" height="392" alt="image" src="https://github.com/user-attachments/assets/79b16e3f-8788-424f-8557-2994b116bb04" />

Verified Suricata configuration and successfully loaded the Emerging Threats rule set, confirming the IDS engine is ready to analyze network traffic.

<img width="1071" height="282" alt="image" src="https://github.com/user-attachments/assets/017997f9-f24e-48c9-bcb0-9f8605e71cff" />

eve.json — structured JSON event log; best for SIEM ingestion and detailed analysis
fast.log — quick human-readable alert summaries
stats.log — performance and traffic statistics about Suricata itself
suricata.log — Suricata service/runtime messages, warnings, and startup/debug info


<img width="1760" height="316" alt="image" src="https://github.com/user-attachments/assets/05178bfc-358f-4779-9e5f-61dbf7d7c821" />

Reviewed Suricata runtime logs to confirm the IDS engine successfully loaded rule sets and initialized packet inspection threads on the network interface.

<img width="1604" height="166" alt="image" src="https://github.com/user-attachments/assets/96696a68-6055-49fd-9f9a-552864c25d01" />

Triggered a Suricata detection by generating test IDS traffic and verified that the Emerging Threats rule set successfully identified and logged potentially malicious network activity.

<img width="1270" height="291" alt="image" src="https://github.com/user-attachments/assets/e19ba46f-4ece-4110-870a-e6e25bf633f7" />

Implemented custom Suricata detection rules to identify ICMP, SSH, and HTTP traffic directed toward the protected network, demonstrating how IDS signatures can be tailored to detect specific activity within a monitored environment.


<img width="1919" height="976" alt="image" src="https://github.com/user-attachments/assets/89f55483-442f-4dd7-9771-3be532dc6841" />

Configured Suricata to load both the Emerging Threats rule set and custom local detection rules, enabling the IDS to apply community signatures alongside user-defined alerts.

<img width="1361" height="333" alt="image" src="https://github.com/user-attachments/assets/2d68bd5d-7cdc-46b9-9903-bb1ca92535ae" />

Suricata configuration validation completed successfully, confirming that both default and custom rule sets were correctly loaded and the IDS engine can start without errors.



<img width="1919" height="480" alt="image" src="https://github.com/user-attachments/assets/e7f52186-2d8d-4ece-979f-d45668c2935c" />

<img width="652" height="241" alt="image" src="https://github.com/user-attachments/assets/ae075191-ec86-4211-840d-1945b3199df0" />

Caption:
Suricata detecting multiple network events in real time as test traffic is generated from a separate terminal.

Description:
While monitoring the Suricata alert log using tail -f /var/log/suricata/fast.log, test traffic was generated from another terminal to validate the IDS rule set. Activities such as ICMP pings and SSH connection attempts were initiated toward the Suricata-monitored host. As packets traversed the network interface, Suricata inspected them against its loaded signature rules and produced alerts that appeared immediately in the fast.log output. This demonstrates Suricata’s ability to perform real-time packet inspection and generate alerts when traffic matches defined detection signatures.

<img width="1915" height="1037" alt="image" src="https://github.com/user-attachments/assets/3d18f918-a781-4ec3-afc5-8cf4d9b0e929" />

Caption:
Viewing Suricata’s eve.json output, which contains detailed structured event data in JSON format but is difficult to interpret in raw form.

Description:
The eve.json file stores Suricata’s full event output using structured JSON logs. Unlike fast.log, which provides concise human-readable alerts, eve.json captures detailed telemetry such as packet statistics, protocol metadata, flow information, and alert data. However, when viewed directly with commands like cat, the JSON output appears as dense, unformatted text that is difficult to read or analyze manually. Tools such as jq can be used to parse and format this structured data, allowing specific fields (such as alerts, source IPs, or protocol information) to be extracted and displayed in a more readable form.

<img width="930" height="245" alt="image" src="https://github.com/user-attachments/assets/caf96f09-c83a-4867-9b8c-f16554e2955b" />

<img width="1249" height="641" alt="image" src="https://github.com/user-attachments/assets/4446bf88-8f18-498c-a4d3-1fcd989a688f" />


Caption:
Using jq to parse Suricata’s eve.json log and filter only alert events while generating ICMP traffic from a separate terminal. SIMILARLY SSH

Description:
To make Suricata’s structured JSON logs easier to analyze, the jq utility was used to filter specific event types from the eve.json file. The command shown pipes the live log output into jq, selecting only entries where the field event_type equals "alert". This allows alerts to be displayed in a readable, structured format while ignoring other telemetry such as statistics or flow records.

In the second terminal, ICMP traffic was generated by sending ping requests to the Suricata-monitored host. As packets were inspected by the IDS engine, matching rules triggered alerts that were immediately displayed in the filtered JSON output.

Command Syntax Breakdown:
sudo tail -f /var/log/suricata/eve.json | jq 'select(.event_type=="alert")'

tail -f /var/log/suricata/eve.json
Streams the Suricata JSON log file in real time as new events are written.

|
The pipe operator sends the output of tail into another program for processing.

jq
A command-line JSON processor used to parse and filter structured log data.

select(.event_type=="alert")
Filters the JSON objects and prints only those where the field event_type equals "alert", effectively isolating IDS detection events from other log entries.


<img width="1919" height="956" alt="image" src="https://github.com/user-attachments/assets/33f244dd-cbda-4bae-8a1e-8f3a73b39c48" />


Caption:
Configured Wazuh to ingest Suricata alerts by monitoring the eve.json log file.

Description:
A <localfile> entry was added to ossec.conf to allow the Wazuh manager to read Suricata’s eve.json output. This enables Suricata IDS alerts to be forwarded into Wazuh for centralized monitoring and analysis in the SIEM dashboard.


<img width="1919" height="920" alt="image" src="https://github.com/user-attachments/assets/175371e3-835a-48e9-aac8-9540c000512e" />

<img width="1094" height="803" alt="image" src="https://github.com/user-attachments/assets/6b48ecdf-3ac6-4d91-9da5-ee66f2026d53" />

<img width="672" height="510" alt="image" src="https://github.com/user-attachments/assets/a3c21b84-7b33-49f8-9de7-ddcbd7d086e3" />

conduct ssh, see alerts in ossec.log, and integrated within wazuh

The Wazuh Discover dashboard is used to filter and analyze security events indexed in wazuh-alerts-*. By applying a filter on the rule.groups field with the value suricata, only alerts generated by Suricata IDS are displayed. This allows security analysts to quickly isolate network intrusion detection events from other system logs such as PAM or syslog, confirming that Suricata alerts are successfully ingested and correlated within the Wazuh SIEM platform.



more testing



brute force ssh
for i in {1..30}; do ssh fakeuser@192.168.122.25; done



