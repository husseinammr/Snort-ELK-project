 # Autonomous Threat Detection & Real-Time SIEM Monitoring System
### Integrated Security Operations Center (SOC) Simulation Lab with Snort IDS & ELK Stack

---

## 📋 Overview
This repository contains a production-ready deployment of a containerized Security Operations Center (SOC) infrastructure. The project demonstrates the execution of live Network Intrusion Detection (IDS) combined with real-time Security Information and Event Management (SIEM). 

By leveraging Snort to inspect raw network traffic and generating defensive signature alerts, this environment automates data ingestion, log parsing, and semantic multi-field search through the ELK Stack (Elasticsearch, Logstash, Kibana).

---

## 🛠 System Architecture & Data Flow

The architecture is built natively around a modular enterprise logging pipeline:

1. Traffic Analysis & Detection (Snort): Monitors specific network interfaces against user-defined attack signatures (local.rules) and writes alerts immediately into a structured alert.ids log file.
2. Log Forwarding (Filebeat): Actively monitors and streams the live Snort alert log file to avoid I/O bottlenecks.
3. Data Parsing & Normalization (Logstash): Ingests the raw, unstructured alert blocks and applies customized Grok Filters to break down metadata (Source IPs, Destination IPs, Ports, Alert Types, Subnets, and Timestamps) into explicit JSON keys.
4. Storage & Indexing (Elasticsearch): Stores normalized data packets inside schema-optimized document indices allowing microsecond response queries.
5. Operational Visualization (Kibana): Aggregates indexed entries to construct security operation metrics dashboards for triage and analysis.

---

## 📁 Repository & Project Structure

The project directory consists of the following foundational components:

* **docker-compose.yml**: Provisions and networks isolated microservice containers for Elasticsearch, Logstash, and Kibana with strictly defined memory configurations.
* **filebeat.yml**: Configures the high-performance harvesting paths to securely relay live Snort logs over TCP/Logstash pipelines.
* **logstash-pipeline.conf**: The extraction engine applying data patterns to transform unstructured alert sequences into individual indexed network attributes.
* **local.rules**: Custom deployment signatures written manually to track localized attack matrices (e.g., Meterpreter payloads, internal subverted mapping, HTTP voluREADME.md
* **README.md**: Architectural blueprint and onboarding manual.

---

## 🔒 Custom Snort Rule Examples Implemented
The system utilizes explicit detection matrices inside the local.rules layer to flag malicious vectMeterpreter Session Activit Catches shell callbacks on critical commanMalicious Payload Vectors:yload Vectors:yload Vectors:** Flags explicit delivery attempts (e.g., HTA or weaponized script transfers across interVolumetric Network Anomalies:ork Anomalies:** Identifies anomalous connection spikes or horizontal host mapping.

---

## 🚀 Deployment & Initialization Guide

Follow these steps to launch the core environment:

### 1. Spin Up the ELK Infrastructure
From your server terminal, enter your working directory and initiate the microservices in detached background mode:
`bash
cd ~/idas-lab
docker-compose up -d

 2. Verify Container Execution
​Ensure all three instances (Elasticsearch, Logstash, Kibana) are fully operational and healthy:

docker ps

 3. Initialize the Logging Stream
​Deploy your local Snort environment to evaluate the ruleset against live traffic and pipe alerts seamlessly:

sudo snort -A fast -c /etc/snort/snort.conf -i <your_network_interface>

4. Visual Dashboard Triage
​Open your browser and navigate to the Kibana console:
​URL: http://localhost:5601 (or your specific Server IP)
​Create an Index Pattern for logstash-* under Stack Management to begin triaging normalized data fields inside the Discover tab.

​🛡️ Key Cybersecurity Insights Demonstrated
​Advanced Data Ingestion: Automating data flows from lower-level OS logging devices to centralized cloud analytics structures.
​Log Normalization Mastery: Converting raw network strings into parsed searchable components for optimized investigative workflows.
​Signature Engineering: Developing custom IDS patterns to harden internal perimeters against modern cyber threats.
