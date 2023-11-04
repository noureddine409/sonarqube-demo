# Installation de SonarQube dans Azure VM

Ce guide vous guidera à travers le processus de création d'une machine virtuelle (VM) Azure et de l'installation de SonarQube dessus. SonarQube est une plateforme open source qui vous permet d'inspecter en continu et d'améliorer la qualité de votre code.

## Prérequis

1. Compte Azure : Vous aurez besoin d'un compte Azure actif pour créer une machine virtuelle.
2. Une compréhension de base des services Azure et des machines virtuelles.

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

