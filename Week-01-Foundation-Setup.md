# Week 1: Foundation Setup & Environment

## 🎯 Weekly Goals

- Set up OpenPI development environment
- Join Noisebridge community
- Understand basic robotics concepts
- Begin hardware fundamentals

## 📅 Schedule

- **Monday**: Environment setup, community joining
- **Tuesday**: OpenPI installation and first run
- **Wednesday**: Basic robotics concepts study
- **Thursday**: Hardware fundamentals research
- **Friday**: First Noisebridge visit
- **Weekend**: Documentation and planning

## 🛠️ Technical Tasks

### Day 1-2: Environment Setup

- [ ] **Install Ubuntu 22.04** (WSL2, VM, or dual boot)
- [ ] **Install NVIDIA CUDA toolkit** (if using GPU)
- [ ] **Install Python 3.8+** and pip
- [ ] **Install uv package manager**:
  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```
- [ ] **Clone OpenPI repository**:
  ```bash
  git clone https://github.com/Physical-Intelligence/openpi.git
  cd openpi
  uv sync
  ```

### Day 3-4: OpenPI Basics

- [ ] **Run first inference example**:
  ```bash
  uv run examples/download_checkpoint.py --config_name pi05_droid
  uv run examples/run_inference.py --config_name pi05_droid
  ```
- [ ] **Understand OpenPI architecture**:
  - Vision-Language-Action (VLA) models
  - Flow matching vs autoregressive models
  - Policy inference pipeline
- [ ] **Read OpenPI documentation** and examples
- [ ] **Set up development environment** (VS Code, Jupyter, etc.)

### Day 5-7: Community & Hardware

- [ ] **Join Noisebridge Discord**: https://discord.gg/GtpDdX5
- [ ] **Attend Circuit Hacking Monday** (7:00pm)
- [ ] **Research robot hardware**:
  - Robot arm specifications
  - Camera requirements
  - Sensor integration
- [ ] **Study basic electronics**:
  - Resistors, capacitors, sensors
  - Arduino basics
  - Motor control fundamentals

## 📚 Learning Resources

### **Reading Materials**

- [OpenPI Repository](https://github.com/Physical-Intelligence/openpi)
- [Noisebridge Wiki](https://www.noisebridge.net/wiki/Noisebridge)
- [Arduino Getting Started](https://www.arduino.cc/en/Guide/HomePage)
- [Robot Kinematics Basics](https://modernrobotics.northwestern.edu/)

### **Video Content**

- [OpenPI Introduction](https://github.com/Physical-Intelligence/openpi)
- [Arduino Tutorial Series](https://www.youtube.com/playlist?list=PLGs0VKk2DiYw-L-RibttcvK-WBZm8WLEP)
- [Noisebridge Tour Video](https://www.noisebridge.net/wiki/Noisebridge)

## 🎯 Deliverables

### **Technical Deliverables**

- [ ] Working OpenPI environment
- [ ] First successful inference run
- [ ] Basic understanding of VLA models
- [ ] Development environment configured

### **Community Deliverables**

- [ ] Active Noisebridge Discord member
- [ ] Attended first Circuit Hacking Monday
- [ ] Introduced yourself to community
- [ ] Set up project documentation

### **Learning Deliverables**

- [ ] Notes on OpenPI architecture
- [ ] Basic electronics knowledge
- [ ] Understanding of robot hardware requirements
- [ ] First week progress documented

## 🔍 Assessment Criteria

### **Technical Skills**

- Can run OpenPI inference examples
- Understands basic model architecture
- Has working development environment
- Can troubleshoot basic issues

### **Community Engagement**

- Active in Noisebridge Discord
- Attended community events
- Introduced project to community
- Building relationships with members

### **Learning Progress**

- Documented learning journey
- Created study notes
- Identified knowledge gaps
- Planned next week's focus

## 🚨 Common Issues & Solutions

### **Installation Issues**

- **CUDA not found**: Install NVIDIA drivers and CUDA toolkit
- **uv sync fails**: Remove .venv and try again
- **Permission errors**: Check file permissions and ownership

### **OpenPI Issues**

- **Model download fails**: Check internet connection and HuggingFace login
- **Inference errors**: Verify GPU memory and model compatibility
- **Import errors**: Ensure all dependencies are installed

### **Community Issues**

- **Discord access**: Check invitation link and account setup
- **Event attendance**: Verify times and locations
- **Network issues**: Test connectivity and firewall settings

## 📝 Daily Checklist

### **Monday**

- [ ] Set up Ubuntu environment
- [ ] Install basic development tools
- [ ] Join Noisebridge Discord
- [ ] Plan week's activities

### **Tuesday**

- [ ] Install OpenPI and dependencies
- [ ] Run first inference example
- [ ] Document any issues encountered
- [ ] Research OpenPI architecture

### **Wednesday**

- [ ] Study robotics fundamentals
- [ ] Learn basic electronics concepts
- [ ] Practice with Arduino examples
- [ ] Update learning notes

### **Thursday**

- [ ] Research robot hardware specifications
- [ ] Study camera and sensor requirements
- [ ] Plan hardware projects
- [ ] Prepare for Noisebridge visit

### **Friday**

- [ ] Visit Noisebridge (272 Capp Street)
- [ ] Attend Circuit Hacking Monday
- [ ] Meet community members
- [ ] Get hands-on with hardware

### **Weekend**

- [ ] Document week's progress
- [ ] Plan next week's activities
- [ ] Update project documentation
- [ ] Prepare for Week 2

## 🎯 Success Metrics

### **Technical Success**

- OpenPI environment working
- First inference successful
- Development tools configured
- Basic understanding of concepts

### **Community Success**

- Active Discord participation
- Attended community events
- Built relationships with members
- Contributed to discussions

### **Learning Success**

- Documented learning journey
- Identified knowledge gaps
- Prepared for next week
- Built foundation for growth

## 📞 Support Resources

### **Technical Support**

- OpenPI GitHub Issues
- Noisebridge Discord #tech-support
- Community forums and documentation
- Online tutorials and guides

### **Community Support**

- Noisebridge Discord community
- Circuit Hacking Monday mentors
- Community members and volunteers
- Online robotics communities

---

**Next Week**: Week 2 - Basic Hardware Integration
