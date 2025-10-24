# Ubuntu Installation Guide for OpenPI Robotics Development

## 🎯 **Overview: Two Installation Options**

### **Option 1: Dual Boot (Recommended for Full Performance)**
- **Pros**: Full hardware access, maximum performance, native Linux experience
- **Cons**: Requires disk partitioning, boot management
- **Best For**: Primary development machine, maximum GPU performance

### **Option 2: WSL2 (Windows Subsystem for Linux)**
- **Pros**: No disk partitioning, easy setup, Windows compatibility
- **Cons**: Limited GPU access, some performance overhead
- **Best For**: Learning environment, Windows-heavy workflows

---

## 🚀 **OPTION 1: DUAL BOOT INSTALLATION**

### **Prerequisites**
- Windows 10/11 with at least 100GB free space
- USB drive (8GB+)
- Internet connection
- Backup important data

### **Step 1: Prepare Your System**

#### **1.1 Create System Backup**
```bash
# Backup important files to external drive
# Use Windows Backup or third-party tools like Macrium Reflect
```

#### **1.2 Disable Secure Boot (Temporary)**
1. Restart computer and enter BIOS/UEFI (F2, F12, Del during boot)
2. Find "Secure Boot" in Security settings
3. Disable Secure Boot
4. Save and exit

#### **1.3 Disable Fast Startup**
1. Open Control Panel → Power Options
2. Click "Choose what the power buttons do"
3. Uncheck "Turn on fast startup"
4. Save changes

#### **1.4 Create Disk Space**
1. Open Disk Management (diskmgmt.msc)
2. Right-click on your main drive
3. Select "Shrink Volume"
4. Shrink by at least 100GB (recommend 200GB+)
5. Leave the space as "Unallocated"

### **Step 2: Create Ubuntu Bootable USB**

#### **2.1 Download Ubuntu 22.04 LTS**
- Go to: https://ubuntu.com/download/desktop
- Download Ubuntu 22.04.3 LTS (Long Term Support)
- File size: ~4.7GB

#### **2.2 Create Bootable USB**
**Using Rufus (Windows):**
1. Download Rufus: https://rufus.ie/
2. Insert USB drive
3. Open Rufus
4. Select your USB drive
5. Click "SELECT" and choose Ubuntu ISO
6. Partition scheme: GPT
7. Target system: UEFI
8. File system: FAT32
9. Click "START"

**Using Balena Etcher (Cross-platform):**
1. Download Etcher: https://www.balena.io/etcher/
2. Select Ubuntu ISO
3. Select USB drive
4. Click "Flash!"

### **Step 3: Install Ubuntu**

#### **3.1 Boot from USB**
1. Insert USB drive
2. Restart computer
3. Press F12/F2 during boot to access boot menu
4. Select USB drive
5. Choose "Try Ubuntu" or "Install Ubuntu"

#### **3.2 Installation Process**
1. **Welcome**: Select language and keyboard layout
2. **Updates**: Check "Download updates while installing"
3. **Installation Type**: Choose "Something else" for manual partitioning
4. **Partitioning**:
   - Select the unallocated space
   - Create root partition: `/` (50GB, ext4)
   - Create home partition: `/home` (remaining space, ext4)
   - Create swap partition: 8GB (if RAM < 16GB)
5. **Boot Loader**: Install to `/dev/sda` (main drive)
6. **User Info**: Create username and password
7. **Install**: Click "Install Now"

#### **3.3 Post-Installation Setup**
```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install essential tools
sudo apt install -y curl wget git vim build-essential

# Install NVIDIA drivers (if applicable)
sudo ubuntu-drivers autoinstall

# Reboot
sudo reboot
```

---

## 🖥️ **OPTION 2: WSL2 INSTALLATION**

### **Prerequisites**
- Windows 10 version 2004+ or Windows 11
- Administrator privileges
- Internet connection

### **Step 1: Enable WSL2**

#### **1.1 Enable Windows Features**
```powershell
# Run PowerShell as Administrator
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

#### **1.2 Restart Computer**
```bash
# Restart required after enabling features
```

#### **1.3 Set WSL2 as Default**
```powershell
# Run PowerShell as Administrator
wsl --set-default-version 2
```

### **Step 2: Install Ubuntu**

#### **2.1 Install from Microsoft Store**
1. Open Microsoft Store
2. Search for "Ubuntu 22.04 LTS"
3. Click "Install"
4. Wait for download and installation

#### **2.2 Alternative: Command Line Installation**
```powershell
# Install Ubuntu 22.04
wsl --install -d Ubuntu-22.04
```

### **Step 3: Initial Ubuntu Setup**

#### **3.1 Launch Ubuntu**
1. Search "Ubuntu" in Start menu
2. Click to launch
3. Wait for installation to complete
4. Create username and password

#### **3.2 Update System**
```bash
# Update package lists
sudo apt update

# Upgrade packages
sudo apt upgrade -y

# Install essential tools
sudo apt install -y curl wget git vim build-essential
```

---

## 🔧 **POST-INSTALLATION SETUP FOR OPENPI**

### **Step 1: Install Development Tools**

#### **1.1 Install Python and uv**
```bash
# Install Python 3.10+
sudo apt install -y python3.10 python3.10-venv python3-pip

# Install uv (recommended package manager)
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc

# Verify installation
uv --version
```

#### **1.2 Install CUDA (for NVIDIA GPUs)**
```bash
# Add NVIDIA repository
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-keyring_1.0-1_all.deb
sudo dpkg -i cuda-keyring_1.0-1_all.deb
sudo apt update

# Install CUDA toolkit
sudo apt install -y cuda-toolkit-12-2

# Add to PATH
echo 'export PATH=/usr/local/cuda-12.2/bin:$PATH' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=/usr/local/cuda-12.2/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc
source ~/.bashrc
```

#### **1.3 Install ROS 2 Humble**
```bash
# Add ROS 2 repository
sudo apt install -y software-properties-common
sudo add-apt-repository universe
sudo apt update && sudo apt install -y curl gnupg lsb-release

# Add ROS 2 GPG key
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

# Install ROS 2
sudo apt update
sudo apt install -y ros-humble-desktop python3-rosdep
sudo rosdep init
rosdep update
```

### **Step 2: Install OpenPI**

#### **2.1 Clone OpenPI Repository**
```bash
# Create development directory
mkdir -p ~/robotics/openpi
cd ~/robotics/openpi

# Clone repository
git clone https://github.com/Physical-Intelligence/openpi.git
cd openpi

# Install dependencies
uv sync
```

#### **2.2 Verify Installation**
```bash
# Test OpenPI installation
python -c "import openpi; print('OpenPI installed successfully!')"

# Test CUDA (if applicable)
python -c "import torch; print(f'CUDA available: {torch.cuda.is_available()}')"
```

---

## 🛠️ **HARDWARE INTEGRATION SETUP**

### **Step 1: Install Arduino IDE**
```bash
# Download Arduino IDE
wget https://downloads.arduino.cc/arduino-ide/arduino-ide_2.2.1_Linux_64bit.AppImage
chmod +x arduino-ide_2.2.1_Linux_64bit.AppImage

# Create desktop shortcut
sudo mv arduino-ide_2.2.1_Linux_64bit.AppImage /opt/arduino-ide
sudo ln -s /opt/arduino-ide /usr/local/bin/arduino-ide
```

### **Step 2: Install 3D Printing Software**
```bash
# Install PrusaSlicer
sudo apt install -y prusa-slicer

# Install FreeCAD
sudo apt install -y freecad

# Install OpenSCAD
sudo apt install -y openscad
```

### **Step 3: Install Development Tools**
```bash
# Install VS Code
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/trusted.gpg.d/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'

sudo apt update
sudo apt install -y code

# Install Git configuration
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

---

## 🚨 **TROUBLESHOOTING**

### **Common Issues**

#### **Dual Boot Issues**
```bash
# Fix GRUB bootloader
sudo update-grub
sudo grub-install /dev/sda

# Fix Windows boot
# Boot from Windows recovery USB
# Run: bootrec /fixmbr
# Run: bootrec /fixboot
```

#### **WSL2 Issues**
```powershell
# Reset WSL2
wsl --shutdown
wsl --unregister Ubuntu-22.04
wsl --install -d Ubuntu-22.04
```

#### **CUDA Issues**
```bash
# Check NVIDIA driver
nvidia-smi

# Reinstall CUDA
sudo apt remove --purge cuda-toolkit-12-2
sudo apt install -y cuda-toolkit-12-2
```

---

## 📋 **VERIFICATION CHECKLIST**

### **System Requirements Met**
- [ ] Ubuntu 22.04 LTS installed
- [ ] Python 3.10+ available
- [ ] CUDA toolkit installed (if NVIDIA GPU)
- [ ] ROS 2 Humble installed
- [ ] OpenPI repository cloned
- [ ] Development tools installed

### **Hardware Integration Ready**
- [ ] Arduino IDE installed
- [ ] 3D printing software installed
- [ ] VS Code configured
- [ ] Git configured
- [ ] USB devices recognized

### **OpenPI Development Ready**
- [ ] OpenPI dependencies installed
- [ ] CUDA working (if applicable)
- [ ] ROS 2 environment sourced
- [ ] Development directory structure created

---

## 🎯 **NEXT STEPS**

1. **Complete Installation**: Choose your preferred method
2. **Follow Week 1 Guide**: Start with foundation setup
3. **Join Community**: Connect with Noisebridge and OpenPI communities
4. **Begin Hardware Integration**: Start Week 2-3 learning plans

**Ready to begin your OpenPI robotics journey!** 🚀
