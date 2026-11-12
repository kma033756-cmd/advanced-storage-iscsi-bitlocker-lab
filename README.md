# Advanced Storage Architecture, iSCSI, BitLocker, & RAID-5 Lab (`ETHA.com`)

## 📌 Project Overview
This repository documents enterprise storage configuration and data security implementations on Windows Server. It covers iSCSI Target Server deployment, Multi-Path Input/Output (MPIO) redundancy, BitLocker volume encryption with key backup, resilient Storage Spaces (Mirrored virtual disks), and dynamic RAID-5 fault-tolerant storage solutions.

## 🏗️ Environment Architecture
* **Storage Provider / Target Server:** `STO-CORE` / `STO-SVR1` (`ETHA.com`)
* **Client Initiator:** `STO-CL1` (`172.16.0.11`)
* **Core Management Tools:** Server Manager, Computer Management (Disk Management), PowerShell ISE (`manage-bde`, iSCSI cmdlets)
* **Domain Functional Level:** Windows Server 2025

---

## ⚙️ Key Tasks & Technical Implementation

### 1. iSCSI Target Storage Deployment & Provisioning
* Deployed the **iSCSI Target Server** role and **Windows Server Backup** features on server nodes.
* Created and formatted multiple iSCSI virtual disks (`.vhdx`) stored under `C:\iSCSIVirtualDisks` on `STO-CORE`.
* Configured iSCSI access servers and targets mapped using IQNs, IP addresses (`172.16.0.10`, `172.16.0.11`), and DNS names (`sto-cl1.etha.com`).

### 2. Multi-Path Input/Output (MPIO) & High Availability
* Installed and configured **Multi-Path Input/Output (MPIO)** features to ensure high availability and load balancing across network storage paths.
* Connected client initiators to discover targets and validated persistent storage connectivity across restarts.

### 3. BitLocker Drive Encryption & Security
* Enabled **BitLocker Drive Encryption** on fixed data volumes (`Encrypted Volume G:`) utilizing XTS-AES 128 encryption.
* Secured recovery keys by backing them up to text files in secure lab paths (`C:\LabFiles\Chapter05`) and verified encryption statuses via PowerShell (`manage-bde -status`).

### 4. Storage Spaces & Fault-Tolerant Mirroring
* Created a storage pool (`StoragePool1`) using pooled physical disks on `STO-SVR1`.
* Provisioned a thin-provisioned **Mirrored Virtual Disk** (`VirtualDisk1`) to provide high data availability and redundancy.
* Simulated a physical disk removal/failure and verified automated system rebuilding and data accessibility.

### 5. Dynamic RAID-5 Volume Configuration & Resilience
* Configured a dynamic **RAID-5 volume** across multiple physical disks providing distributed parity.
* Calculated raw vs usable capacity metrics (accounting for parity overhead across the smallest disk sizes).
* Simulated disk failure and performed online resynchronization, verifying that user data remained fully accessible during the rebuild process.
