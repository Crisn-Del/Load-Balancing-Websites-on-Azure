# Load-Balancing-Websites-on-Azure
This project demonstrates how to design and deploy an **internal load balancing solution** on Microsoft Azure using multiple services
# Project 2: Load Balancing Websites on Azure

This project demonstrates how to design and deploy an **internal load balancing solution** on Microsoft Azure using multiple services:  
- Azure Bastion  
- Azure Virtual Machines (IIS Webservers)  
- Azure Virtual Networks + Peering  
- Azure Load Balancer  
- Azure Private DNS

- <img width="762" height="555" alt="image" src="https://github.com/user-attachments/assets/efbf6790-b22f-47eb-99e9-136c645b4561" />


The goal is to distribute traffic between **two IIS webservers** in different availability zones, and demonstrate that a client VM in another VNet can reach both servers through the load balancer.

---

## 🎯 Objectives
- Deploy a **secure architecture** using private networking and Azure Bastion for remote management.
- Configure **two VNets** with peering and subnets.
- Deploy **two IIS-based webservers** into a load balancer backend pool.
- Use **Azure Private DNS** for internal resolution.
- Verify load balancing by connecting from a client VM.

---

## 📂 Repository Layout
- `topology/` → network diagram  
- `azure-resources/` → text configs and notes for resource creation  
- `webservers/` → HTML/IIS default pages for webserver1 and webserver2  
- `dns/` → private DNS zone config  
- `notes/` → instructions and lab notes  

---

## 🚀 Azure Components

### Resource Group
- Name: `MST300-project2-rg`

### Virtual Networks
- **MST300-vnet1** → 2 subnets (`vnet1-subnet1`, `AzureBastionSubnet`)  
- **MST300-vnet2** → 1 subnet (`vnet2-subnet1`)  

### Virtual Network Peering
- Configured between `MST300-vnet1` and `MST300-vnet2`.

### Load Balancer
- Name: `MST300-lb` (internal)  
- Backend Pool: `MST300-BackendPool`  
- Health Probe: `MST300-HealthProbe` (HTTP, port 80, interval 15s)  
- Rule: `MST300-HTTPRule` (TCP, port 80, timeout 15 min, TCP reset enabled)  

### Bastion
- Name: `MST300-BastionHost`  
- Subnet: `AzureBastionSubnet`  
- Public IP: `MST300-BastionIP`  

### Webservers
- **webserver1-vm** (Availability Zone 1)  
  - IIS default page → title: *studentID’s Windows Server*  
  - Body: *This webpage is hosted on webserver1-vm*  

- **webserver2-vm** (Availability Zone 2)  
  - IIS default page → title: *studentID’s WebPage*  
  - Body: *This webpage is hosted on webserver2-vm*  

---

## 🧪 Testing
1. Connect to **client VM** in `MST300-vnet2` using Bastion.  
2. Open a browser and go to the internal LB private IP.  
3. Refresh multiple times → you should see responses alternating between `webserver1-vm` and `webserver2-vm`.  

---

## 📝 Notes
- Be mindful of **Azure Bastion costs** — delete resources when not in use.  
- Use your assigned network address space (from Blackboard).  
- Ensure **no overlapping subnets** across VNets.  

---
