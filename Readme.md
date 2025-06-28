# 🏨 Hotel Network Infrastructure – CIE 447 (Spring 2025)

## 📌 Project Overview
This project involves the design and implementation of a hierarchical, multi-floor network infrastructure for a hotel using **Cisco Packet Tracer**. The network is structured to support departmental segmentation, inter-floor routing, server configuration, and DHCP services, while remaining scalable and adaptable to future changes, including departmental relocations.

## 🗂️ Network Architecture

### 📶 Floors and Departments
- **1st Floor**: Reception (VLAN 80), Store (VLAN 70), Logistics (VLAN 60)
- **2nd Floor**: Finance (VLAN 50), HR (VLAN 40), Sales (VLAN 30)
- **3rd Floor**: IT (VLAN 10), Admin (VLAN 20)

Each floor is connected to a dedicated router placed in the IT department via **serial DCE links**. All departments are assigned their own VLANs and subnets from the `192.168.2.0/24` address space.

### 🧩 Subnetting Plan
| Department | VLAN | Subnet             | Gateway         |
|------------|------|--------------------|-----------------|
| IT         | 10   | 192.168.2.0/26     | 192.168.2.1     |
| Sales      | 30   | 192.168.2.32/27    | 192.168.2.33    |
| Reception  | 80   | 192.168.2.64/27    | 192.168.2.65    |
| Finance    | 50   | 192.168.2.96/27    | 192.168.2.97    |
| Store      | 70   | 192.168.2.120/29   | 192.168.2.121   |
| HR         | 40   | 192.168.2.128/28   | 192.168.2.129   |
| Logistics  | 60   | 192.168.2.136/29   | 192.168.2.137   |
| Admin      | 20   | 192.168.2.160/27   | 192.168.2.161   |

### 🌐 Inter-Router Links
| Link    | Subnet             | IPs Used                  |
|---------|--------------------|---------------------------|
| R1–R2   | 192.168.2.148/30   | 192.168.2.149 / .150      |
| R2–R3   | 192.168.2.152/30   | 192.168.2.153 / .154      |
| R1–R3   | 192.168.2.156/30   | 192.168.2.157 / .158      |
| R2–R4   | 192.168.2.192/30   | 192.168.2.193 / .194 (Sales HQ) |

---

## ⚙️ Configuration Summary

### 🖥️ Servers
| Server Type  | VLAN | IP Address       |
|--------------|------|------------------|
| DNS Server   | 20   | 192.168.2.114    |
| Web Server   | 50   | 192.168.2.98     |
| DHCP Server  | 80   | 192.168.2.66     |
| DHCP Server  | 40   | 192.168.2.130    |
| DHCP Server  | 10   | 192.168.2.2      |

- `www.hotelservices.com` is hosted on the Finance department's web server.
- The DNS server resolves internal domain names.
- Each floor has a dedicated DHCP server for local IP assignment.

---

## 🔁 Routing Protocol
- **OSPF (Open Shortest Path First)** is used to dynamically advertise all VLAN subnets and interconnect routers across floors and remote branches.
- Configured on all routers using `router ospf 1`.

---

## 🚚 Additional Scenario – Department Relocation

### 🏢 Sales Department
- Relocated to a remote headquarters in another city.
- Connected via router R4 using a new subnet `192.168.2.192/30`.
- Maintains VLAN 30 and its original subnet (`192.168.2.32/27`).

### 🧾 Admin Department
- Moved from the 3rd floor to the 1st floor.
- VLAN 20 and IP scheme preserved (`192.168.2.160/27`).
- Subinterface moved from 3rd-floor router to 1st-floor router.
- DHCP pool transferred to the first-floor DHCP server.

---

## ✅ Testing & Verification

- **Ping Tests** across all VLANs and routers confirm full connectivity.
- **DHCP Assignments** verified for all VLANs.
- **Website** (`www.hotelservices.com`) is accessible from all departments.
- **DNS resolution** functional across network.
- **OSPF routes** confirmed using `show ip route ospf` and `show ip ospf neighbor`.

(*Screenshots included in the project submission folder.*)

---

## 📦 Files Included
- `HotelNetwork.pkt`: Cisco Packet Tracer project file
- `README.md`: Project documentation
- `Screenshots/`: Folder with test results and configurations
- `Report.pdf`: Optional detailed report for submission

---

## 🙋 Contact
**Author:** Ghayth  
**Course:** CIE 447 – Computer Networks  
**Instructor:** Eng. Mohamed

---

