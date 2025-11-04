# Splunk Attack Range: An Expert's Guide

## Introduction

The Splunk Attack Range is an open-source project maintained by the Splunk Threat Research Team. It is a detection development platform that allows you to build a small lab infrastructure, simulate attacks, and forward the data to a Splunk instance. This enables you to develop and test the effectiveness of your detections in a realistic environment.

### Key Features

*   **Rapid Lab Deployment:** Quickly build a lab environment that mimics a production environment.
*   **Attack Simulation:** Use built-in tools like Atomic Red Team and Caldera to generate realistic attack data.
*   **CI/CD Integration:** Seamlessly integrate the Attack Range into your CI/CD pipeline to automate detection testing.
*   **Multi-Cloud Support:** Deploy the Attack Range on AWS, Azure, and GCP.

## Architecture

The Splunk Attack Range is composed of the following components:

*   **Windows Domain Controller:** A Windows Server machine that acts as a domain controller.
*   **Windows Server:** A Windows Server machine that can be used as a target for attack simulations.
*   **Windows Workstation:** A Windows 10 machine that can be used as a target for attack simulations.
*   **Kali Linux:** A preconfigured Kali Linux machine for penetration testing.
*   **Splunk Server:** A Splunk instance that collects and indexes logs from the other components.
*   **Splunk SOAR Server:** A Splunk SOAR instance for security orchestration and automation.
*   **Nginx Server:** A web server that acts as a reverse proxy for the Splunk Server and other components.
*   **Linux Server:** A Linux machine that can be used as a target for attack simulations.
*   **Zeek Server:** A Zeek instance for network security monitoring.
*   **Snort Server:** A Snort instance for intrusion detection.

These components can be added, removed, and configured using the `attack_range.yml` file.

## Usage Guide

This guide will walk you through the process of configuring, building, and running attack simulations with the Splunk Attack Range.

### 1. Installation

The recommended way to install the Attack Range is using Docker. The following instructions are for AWS. For other cloud providers, please refer to the official documentation.

```bash
docker pull splunk/attack_range
docker run -it splunk/attack_range
aws configure
python attack_range.py configure
```

### 2. Configuration

The Attack Range is configured using the `attack_range.yml` file. This file allows you to enable, disable, and configure the different components of the Attack Range.

### 3. Building the Attack Range

To build the Attack Range, run the following command:

```bash
python attack_range.py build
```

### 4. Simulating Attacks

The Attack Range supports different attack simulation engines, including Atomic Red Team and Caldera. To run a simulation, use the `simulate` command.

**Atomic Red Team:**

```bash
python attack_range.py simulate -e ART -te T1003.001 -t ar-win-ar-ar-0
```

**PurpleSharp:**

```bash
python attack_range.py simulate -e PurpleSharp -te T1003.001 -t ar-win-ar-ar-0
```

### 5. Destroying the Attack Range

To destroy the Attack Range, run the following command:

```bash
python attack_range.py destroy
```

## Logging and Data Collection

The Attack Range collects logs from various sources and forwards them to the Splunk instance. The following log sources are collected:

*   Windows Event Logs (`index = win`)
*   Sysmon Logs (`index = win`)
*   Powershell Logs (`index = win`)
*   Aurora EDR (`index = win`)
*   Sysmon for Linux Logs (`index = unix`)
*   Nginx logs (`index = proxy`)
*   Network Logs with Splunk Stream (`index = main`)
*   Attack Simulation Logs from Atomic Red Team and Caldera (`index = attack`)
*   Zeek Logs (`index = zeek`)
*   Snort Logs (`index = snort`)
*   Cisco Secure Endpoint Logs (`index = cisco_secure_endpoint`)
*   CrowdStrike Falcon Logs (`index = crowdstrike_falcon`)
*   Carbon Black Logs (`index = carbon_black_cloud`)

### Dumping Log Data

You can dump log data from the Splunk instance using the `dump` command:

```bash
python attack_range.py dump --file_name attack_data/dump.log --search 'index=win' --earliest 2h
```

### Replaying Log Data

You can replay dumped log data into the Splunk instance using the `replay` command:

```bash
python attack_range.py replay --file_name attack_data/dump.log --source test --sourcetype test
```

## Features

The Splunk Attack Range comes with a variety of features to help you with your detection development workflow.

### Splunk Server

*   **Preconfigured TAs:** The Splunk Server comes with multiple Technical Add-ons (TAs) preconfigured for field extractions.
*   **ESCU App:** The Enterprise Security Content Update (ESCU) App is preinstalled with out-of-the-box Splunk detections.
*   **MLTK:** The Machine Learning Toolkit (MLTK) is preinstalled.
*   **BOTS Datasets:** The Splunk Server comes with pre-indexed BOTS datasets.

### Splunk Enterprise Security

*   Splunk Enterprise Security is a premium security solution that can be enabled in the `attack_range.yml` file. A paid license is required.

### Splunk SOAR

*   Splunk SOAR is a Security Orchestration and Automation platform that can be enabled in the `attack_range.yml` file. A free development license is available.

### Attack Simulation Tools

*   **Atomic Red Team:** A library of simple tests that every security team can execute to test their defenses.
*   **PurpleSharp:** A native adversary simulation tool.
*   **Kali Linux:** A preconfigured Kali Linux machine for penetration testing.
*   **Caldera:** An automated adversary emulation system.

## Support and Contribution

### Support

If you have questions or need support, you can:

*   Join the [#security-research](https://splunk-usergroups.slack.com/archives/C1S5BEF38) room in the [Splunk Slack channel](http://splunk-usergroups.slack.com)
*   Post a question to [Splunk Answers](http://answers.splunk.com)
*   Open a support case on the [Splunk support portal](https://www.splunk.com/) if you are a Splunk Enterprise customer.

### Contribution

We welcome feedback and contributions from the community! Please see our [contribution guidelines](CONTRIBUTING.md) for more information on how to get involved.