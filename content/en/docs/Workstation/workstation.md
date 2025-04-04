# Table of Contents
## 1. Introduction
Mendix Workstation is designed to help you build smarter, faster, and more operator-friendly applications. It enables Mendix cloud applications to directly interact with peripheral devices on a local workstation — without relying on intermediate servers or heavy network traffic.

By connecting applications directly to the PC's local resources, Workstation allows for real-time communication with devices like printers, barcode scanners, smartcard readers, and industrial scales — all from within a Mendix app. This setup ensures low-latency performance and reduces infrastructure complexity.

Workstation is especially valuable in manufacturing and industrial environments where precision, speed, and reliability are key to operator efficiency.
### 1.1 Features

- **Direct Local Device Access**  
  Workstation allows Mendix client applications to send and receive messages directly from the PC’s local hardware.

- **No Server Detour**  
  Communication happens between the client app and local devices — without routing through a central server.

- **Supports Multiple Peripheral Types**  
  - Smartcard Readers (PC/SC)  
  - Serial Port Devices (RS232)  
  - TCP/IP Client/Server (Ethernet)  
  - Bluetooth LE Devices  
  - Local File System  
  - Windows Printers (coming soon)

- **Device Simulation**  
  Useful for development, testing, and demos when real hardware isn’t available. (TCP_IP Server)?
### 1.2 How It Works

Mendix Workstation consists of **three core components**: the **Workstation Management** for centralized configuration, the **Workstation Agent** for real-time communication with local hardware, and the **Workstation Connector** for app integration. Together, they ensure secure, efficient, and scalable interactions between applications and devices.

---

### Workstation Management

**Used by:**  
Central IT and application support teams

The control center provides a centralized interface to **configure and monitor all workstations and devices** across the organization. Whether managing a few stations or hundreds across multiple global sites, administrators can register computers, assign devices, and remotely troubleshoot connection issues — all from the Workstation Management.

This makes it easier to manage a large, diverse fleet of devices without the need for manual setup or on-site support.

---

### Workstation Agent

**Used by:**  
Central IT, support teams, operators, and supervisors

Installed on each local workstation, the **Workstation Agent** acts as a bridge between the Mendix client app and local hardware. It handles the traffic between connected devices and the client application using the configurations provided by the **Workstation Management**.

---

### Workstation Connector (Mendix Module)

**Used by:**  
Mendix developers

The **App Connector** is a plug-and-play Mendix module that allows developers to connect their apps to local devices using [**nanoflows**](https://docs.mendix.com/refguide/nanoflows/). It establishes a connection with the **Workstation Agent**, which acts as the intermediary between the Mendix app and the local devices. Once this connection is established, the module facilitates seamless data exchange by routing messages and events back and forth between the app and the devices.

The connector handles:  
- Connecting to available devices  
- Sending and receiving messages  
- Listening for on-event triggers  
- Disconnecting from devices  

---

Together, these components enable Mendix applications to securely and efficiently integrate with local devices, bridging the gap between digital workflows and physical operations.
## 2. Use Cases & Benefits [WIP]
## 3. Architecture
### 3.1 Overview (Diagram)
### 3.2 Components
#### 3.2.1 WS Management
- Features
- Configurations (create Workspaces, Stations, Devices and Apps)
#### 3.2.2 WS Agent
- Features
- System requirements
- Installation
- Configuration
- Troubleshooting
#### 3.2.3 WS Connector
- Setup
- Configuration
- API Reference
### 3.4 Security
- Overview
- Permissions
- App Security (off, token, Certificate)

## 4. Getting Started

### 4.1 Prerequisites

Before installing Mendix Workstation, ensure the following requirements are met:

- **System Requirements**: <span style="color:red;">[WIP]</span>  
  - Windows 10 or later (64-bit)  
  - Minimum 4 GB RAM (8 GB recommended)  
  - At least 2 GHz dual-core processor  
  - 500 MB of free disk space  

- **Required Permissions**:  
  - Administrator rights to install the Workstation Agent. <span style="color:red;">(Still the case right?)</span>  
  - A Mendix account  
  - Access to the Mendix Workstation Management for configuration.  

- **Network Configuration**:  
  - Ensure the user can access the Mendix cloud.  
  - Open the required ports for communication (e.g., TCP 443 for HTTPS).  
  - Allowlist the Mendix Workstation Agent in any firewall or antivirus software if applicable.  

---

### 4.2 Installation Guide

Follow these steps to install Mendix Workstation:

1. **Download the Installer**:  
   - Visit the official Mendix Workstation page and download the latest version of the installer.<span style="color:red;">[Currently available within the Workstation Management]]</span>

2. **Run the Installer**:  
   - Double-click the downloaded file and follow the on-screen instructions.  
   - Accept the license agreement.<span style="color:red;">[Do we have that at the moment? Stephane demoed it]</span>

3. **Install the Workstation Agent**:  
   The installer will automatically install the Workstation Agent in the Program Files directory and create a configuration folder in ProgramData.
   - Ensure the agent starts running after installation.

4. **Verify Installation**:  
   - During installation, you can choose to run the Workstation Agent immediately after installation by selecting the "run after install" option.  
   - If the Agent is not running, run it and check if it is available in the system tray. Open it and verify that it is working properly.
---

### 4.3 Quick Start Tutorial

#### 4.3.1 Basic Setup

1. **Log In to the Workstation Management**:  
   - Open the Mendix Workstation Management in your browser.  
   - Log in with your Mendix account credentials.

2. **Register Your Station**:  
   - Navigate to the "Station Overview" section and click "Add Station."  
   - Enter a display name for the station and click "Create Station".

3. **Register the Station to the Agent**:  
   - Open the Workstation Agent on the local machine. The Agent will display an input field prompting you to enter the registration token.  
   - In the Workstation Management, retrieve the token by clicking the three dots next to the station and selecting "Register Computer."  
   - Paste the token into the input field in the Workstation Agent to complete the registration.

4. **Test Device Communication**:  
   - Use the Local Device Testing page in the Workstation Management to verify that devices are available and reachable.  
   - Connect to a device and test communication by sending or viewing received data.

---

#### 4.3.2 Build Your First Mendix Application with Workstation

1. **Create a New Mendix App**:  
   - Open Mendix Studio Pro and create a new app using a blank or starter template.

2. **Import the Connector Artifacts**:  
   - Download the **Workstation Connector** and **Interface** modules.  
   - In Studio Pro, go to **App Explorer** > **Import Module Package** and import both modules into your app.  
   - ![Screenshot: Importing Connector Artifacts](path/to/screenshot1.png)

3. **Configure the Application in Workstation Management**:  
   - Navigate to the "Stations" section in the Workstation Management.  
   - Add your application (including localhost for local testing) to the allowed list under the station's configuration.  
   - Click on the three dots next to the application and retrieve the **Access Key**.  
   - ![Screenshot: Adding Application to Allowed List](path/to/screenshot2.png)

4. **Set Up the Shared Secret in the Connector**:   
   - After deploying the app, locate the **Workstation Connector** settings and add the retrieved **Access Key** as the **Shared Secret**.  
   - This ensures valid authentication between the connector and the Workstation Agent.  
   - ![Screenshot: Configuring Shared Secret in Runtime Settings](path/to/screenshot3.png)

5. **Retrieve Devices**:  
   - Use the **DS_Station** nanoflow to retrieve the list of devices connected to the workstation.  
   - Bind the retrieved devices to a data grid or list view in your app.  
   - ![Screenshot: Configuring DS_Station Nanoflow](path/to/screenshot4.png)

6. **Connect to a Device**:  
   - Add a button to your app and configure it to call the **SUB_ConnectToDevice** nanoflow.  
   - Pass the selected device as a parameter to establish a connection.  
   - ![Screenshot: Configuring SUB_ConnectToDevice Nanoflow](path/to/screenshot5.png)

7. **Send a Message to the Device**:  
   - Add another button to call the **SUB_SendMessage** nanoflow.  
   - Use this to send data or commands to the connected device.  
   - ![Screenshot: Configuring SUB_SendMessage Nanoflow](path/to/screenshot6.png)

8. **Disconnect from the Device**:  
   - Add a final button to call the **SUB_Disconnect** nanoflow.  
   - Use this to safely disconnect from the device when done.  
   - ![Screenshot: Configuring SUB_Disconnect Nanoflow](path/to/screenshot7.png)

9. **Run the App Locally**:  
   - Run the app locally in Studio Pro.  
   - Test the functionality by connecting to a device, sending a message, and disconnecting.  
   - ![Screenshot: Running the App Locally](path/to/screenshot8.png)

10. **Verify Results**:  
    - Ensure that the app displays the correct device data and handles communication as expected.

---

### Key Nanoflows Overview

- **DS_Station**: Retrieves devices.  
- **SUB_ConnectToDevice**: Connects to a device.  
- **SUB_SendMessage**: Sends a message to the device.  
- **SUB_Disconnect**: Disconnects from the device.

---

### 4.4 Best Practices

- **Security Recommendations**:  
  - Regularly update the Workstation Agent to the latest version.  
  - Use strong passwords and enable two-factor authentication for Mendix accounts.  

- **Performance Optimization**:  
  - Ensure workstations meet the recommended hardware specifications.  
  - Minimize background processes to improve performance.  

- **Maintenance Guidelines**:  
  - Periodically review and update workstation and device configurations.  
  - Monitor workstation health and resolve any connectivity issues promptly.  

## 5. Troubleshooting
### 5.1 Common Issues
### 5.2 Error Messages
### 5.3 Support Resources

## 6. API Reference
### 6.1 REST API
### 6.2 SDK (if applicable)

## 7. Limitations & Constraints
### 7.1 Technical Limitations
### 7.2 Scalability Considerations
### 7.3 Known Issues

## 8. Licensing
### 8.1 License Types
### 8.2 Pricing
### 8.3 Terms and Conditions

## 9. Updates and Versioning
### 9.1 Version History
### 9.2 Upgrade Process
### 9.3 Deprecation Policy

## 10. Community and Support
### 10.1 Community Forums
### 10.2 Support Channels
### 10.3 Training Resources

## 11. Glossary

## 12. FAQ
