# 🚀 Week 0: VLSI System Design (VSD) Program Foundation & Tool Setup

<div align="center">

![VLSI](https://img.shields.io/badge/VLSI-System%20Design-blue?style=for-the-badge&logo=chip)
![Week](https://img.shields.io/badge/Week-0-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-success?style=for-the-badge)

</div>

Welcome to my **VLSI System Design (VSD) Program** repository! This week focused on setting up the development environment and installing the essential open-source tools that will be used throughout the program. The goal was to create a reliable and efficient workspace for synthesis, simulation, and design tasks.

---

## 🎯 **System and Virtual Machine Configuration**

To ensure optimal performance, I configured a **Virtual Machine (VM)** with the following specifications:

<div align="center">

| **Specification** 💻    | **Details** 📋          |
|-----------------------|-----------------------|
| **Operating System** 🐧  | Ubuntu 20.04+         |
| **RAM** 💾               | 6GB                   |
| **Storage** 💿           | 50GB HDD              |
| **vCPUs** ⚡             | 4                     |

</div>


---

## ⚙️ **Tool Installation & Verification**

The following tools were installed for RTL synthesis, simulation, circuit analysis, and layout design. Below are the installation steps and verification commands.

<div align="center">

```
🧠 Yosys → 📟 Iverilog → 📊 GTKWave → ⚡ Ngspice → 🎨 Magic VLSI → 🌐 OpenLane
```

</div>

---

### 🧠 **1. Yosys – RTL Synthesis Tool**

<details>
<summary><b>Purpose:</b> Converts RTL code into gate-level representations.</summary>

Yosys is a framework for Verilog RTL synthesis, providing synthesis algorithms and optimization passes for digital circuits.

</details>

## ✅ **Yosys Installation**

```bash
# Day 0 - Tools Installation
## Yosys

git clone https://github.com/YosysHQ/yosys.git
cd yosys 
sudo apt install make 
sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
make 
sudo make install
```

## 📷 **Installation Verification**
<p align="center">
  <img src= "https://github.com/Astrophile1509/RISC-V-Tapeout/blob/main/week%200/Images/yosys.png"
       alt="Yosys Installed" width="600"/>
</p>

<div align="center">

✅ **Yosys Successfully Installed**

</div>

---

### 📟 **2. Iverilog – Verilog Simulator**

<details>
<summary><b>Purpose:</b> Compiles and simulates Verilog designs for functional verification.</summary>

Icarus Verilog is a Verilog simulation and synthesis tool that supports the IEEE-1364 Verilog HDL standard.

</details>

## **Iverilog Installation**
```bash
sudo apt-get install iverilog
```

## 📷 **Installation Verification**
<p align="center">
  <img src="https://github.com/Astrophile1509/RISC-V-Tapeout/blob/main/week%200/Images/iverilog.png" 
       alt="Iverilog Installed" width="600"/>
</p>

<div align="center">

✅ **Iverilog Successfully Installed**

</div>

---

### 📊 **3. GTKWave – Waveform Viewer**

<details>
<summary><b>Purpose:</b> Analyzes and visualizes simulation waveforms for debugging.</summary>

</details>

## **GTKWave Installation**
```bash
sudo apt update
sudo apt install gtkwave
```

## 📷 **Installation Verification**
<p align="center">
  <img src="https://github.com/Astrophile1509/RISC-V-Tapeout/blob/main/week%200/Images/gtkwave.png" 
       alt="GTKWave Installed" width="600"/>
</p>

<div align="center">

✅ **GTKWave Successfully Installed**

</div>

---

### ⚡ **4. Ngspice – Circuit Simulator**

<details>
<summary><b>Purpose:</b> Performs analog and mixed-signal circuit simulation.</summary>

Ngspice is a mixed-level/mixed-signal circuit simulator based on Spice3f5, Cider1b1 and Xspice.

</details>

## **Ngspice Installation**
```bash
sudo apt update
sudo apt install ngspice
```

## 📷 **Installation Verification**
<p align="center">
  <img src="https://github.com/Astrophile1509/RISC-V-Tapeout/blob/main/week%200/Images/ngspice.png" 
       alt="ngspice Installed" width="600"/>
</p>

<div align="center">

✅ **Ngspice Successfully Installed**

</div>

---

### 🎨 **5. Magic VLSI – Layout Tool**

<details>
<summary><b>Purpose:</b> Creates, edits, and analyzes VLSI layouts with DRC capabilities.</summary>

Magic VLSI is an open-source VLSI layout tool widely used for IC design, DRC, and visualization.

</details>

## ✅ **Magic VLSI Installation**

[Magic VLSI](http://opencircuitdesign.com/magic/) is an open-source VLSI layout tool widely used for IC design, DRC, and visualization.  

Follow the steps below to install Magic on an Ubuntu/Debian system:

```bash
# Install required dependencies
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install mesa-common-dev libglu1-mesa-dev
sudo apt-get install libncurses-dev

# Clone Magic repository
git clone https://github.com/RTimothyEdwards/magic
cd magic

# Configure build
./configure

# Build Magic
make

# Install system-wide
sudo make install
```

## 📷 **Installation Verification**
<p align="center">
  <img src="https://github.com/Astrophile1509/RISC-V-Tapeout/blob/main/week%200/Images/magic.png" 
       alt="magic vlsi Installed" width="600"/>
</p>

<div align="center">

✅ **Magic VLSI Successfully Installed**

</div>

---

## ✅ **OpenLane Installation**

[OpenLane](https://github.com/The-OpenROAD-Project/OpenLane) is an automated RTL to GDSII flow based on several opensource tools.  

Follow the steps below to install OpenLane on an Ubuntu/Debian system:
## 🐳 **Installing Docker**

<details>
<summary><b>Purpose:</b> Docker provides containerized environment for OpenLane tools.</summary>

Docker ensures consistent tool behavior across different systems and simplifies the installation process.

</details>

### **Step 1: Set Up Docker Repository**
```bash
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

Add Docker's official repository:
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo \"$VERSION_CODENAME\") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

### **Step 2: Install Docker Engine**
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

### **Step 3: Verify Installation**
Run the test image:
```bash
sudo docker run hello-world
```

<div align="center">

✅ **Docker Successfully Installed**

</div>

---

## ⚠️ **Fixing Docker Permissions**

<details>
<summary><b>Important:</b> Required if you encounter "permission denied" errors.</summary>

This step allows running Docker commands without sudo, which is essential for OpenLane operation.

</details>

If you encounter a **"permission denied"** error related to Docker socket access:

### **Add Your User to the Docker Group**
```bash
# Create the docker group (if it doesn't exist)
sudo groupadd docker

# Add your user to the docker group
sudo usermod -aG docker $USER
# Log out and back in for group changes to take effect
reboot
```

<div align="center">

✅ **Docker Permissions Fixed**

</div>

---

## 🧰 **Installing OpenLane**

<details>
<summary><b>Purpose:</b> Complete RTL-to-GDSII automated flow for digital ASIC design.</summary>

OpenLane is an automated RTL to GDSII flow that includes synthesis, placement, routing, and physical verification.

</details>

### **Step 1: Verify Prerequisites**

<div align="center">

| Tool | Purpose | Check Command |
|------|---------|---------------|
| 🔧 **Git** | Version control | `git --version` |
| 🐳 **Docker** | Containerization | `docker --version` |
| 🐍 **Python3** | Scripting | `python3 --version` |
| 📦 **Pip** | Package manager | `python3 -m pip --version` |
| 🛠️ **Make** | Build automation | `make --version` |
| 🔧 **Venv** | Virtual environments | `python3 -m venv -h` |

</div>

Ensure the following tools are installed:
```bash
git --version
docker --version
python3 --version
python3 -m pip --version
make --version
python3 -m venv -h
```

### **Step 2: Update & Install Required Packages**
```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv python3-pip python3-tk curl make git
```

### **Step 3: Clone and Build OpenLane**
```bash
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane
cd OpenLane
make
./venv/bin/ciel ls-remote --pdk-family sky130
./venv/bin/ciel enable --pdk-family sky130 a80ed405766c5d4f21c8bfca84552a7478fe75b2
make test
```

<div align="center">

✅ **OpenLane Successfully Installed**

</div>
</div>

---

<div align="center">

## 🎉 **Installation Complete!**

### **Verification Commands**

```bash
# Test Docker
docker --version

# Test OpenLane
cd $HOME/OpenLane
make test
```

| Component | Status | Version Check |
|-----------|--------|---------------|
| 🐳 **Docker** | ✅ Ready | `docker --version` |
| 🧰 **OpenLane** | ✅ Ready | `cd OpenLane && make test` |

### 🚀 **Ready for RTL-to-GDSII Flow!**

</div>

---

<div align="center">

## 🎉 **Installation Summary**

| Tool | Status | Primary Use |
|------|--------|-------------|
| 🧠 **Yosys** | ✅ Complete | RTL Synthesis |
| 📟 **Iverilog** | ✅ Complete | Verilog Simulation |
| 📊 **GTKWave** | ✅ Complete | Waveform Analysis |
| ⚡ **Ngspice** | ✅ Complete | Circuit Simulation |
| 🎨 **Magic VLSI** | ✅ Complete | Layout Design |
| 🌐 **OpenLane**  |  ✅ Complete  | Automated RTL to GDSII  |

### 🚀 **Environment Ready for VLSI Design Journey!**

</div>

---

<div align="center">

**📂 Repository:** [RISC-V-Tapeout](https://github.com/Astrophile1509/RISC-V-Tapeout)  
**👨‍💻 Author:** [Astrophile1509](https://github.com/Astrophile1509)  
**📚 Program:** VLSI System Design (VSD)

</div>
