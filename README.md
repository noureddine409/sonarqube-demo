# Installing SonarQube on Azure VM

This guide will walk you through the process of creating an Azure Virtual Machine (VM) and installing SonarQube on it. SonarQube is an open-source platform that helps you continuously inspect and improve the quality of your code.

## Prerequisites

1. Azure account: You'll need an active Azure account to create a VM.
2. A basic understanding of Azure services and virtual machines.

## Step 1: Create an Azure VM

```bash
# Log in to Azure
az login

# Create a resource group
az group create --name myResourceGroup --location eastus

# Create a VM
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --admin-username azureuser --generate-ssh-keys

# Open port 9000 for SonarQube
az vm open-port --resource-group myResourceGroup --name myVM --port 9000 --priority 1010

# Connect to your VM via SSH
ssh azureuser@your-vm-ip

# Update your package list and upgrade existing packages
sudo apt update
sudo apt upgrade

# Install OpenJDK 11
sudo apt install openjdk-11-jre-headless

# Download and unzip SonarQube
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-<version>.zip
unzip sonarqube-<version>.zip -d /opt

# Create a symbolic link
sudo ln -s /opt/sonarqube-<version> /opt/sonarqube

# Edit SonarQube configuration
sudo nano /opt/sonarqube/conf/sonar.properties

# Start SonarQube
sudo /opt/sonarqube/bin/linux-x86-64/sonar.sh start

