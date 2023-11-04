# Installation de SonarQube dans Azure VM

Ce guide vous guidera à travers le processus de création d'une machine virtuelle (VM) Azure et de l'installation de SonarQube dessus. SonarQube est une plateforme open source qui vous permet d'inspecter en continu et d'améliorer la qualité de votre code.

## Prérequis

1. Compte Azure : Vous aurez besoin d'un compte Azure actif pour créer une machine virtuelle.
2. Une compréhension de base des services Azure et des machines virtuelles.

## Step 1: Create an Azure VM
<img width="960" alt="Capture" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/f6b0ab70-0761-4787-a752-3060336fc3ed">
<img width="523" alt="Capture2" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/6e19775e-b120-4d28-8f54-84c429d7ac4f">
<img width="627" alt="Capture3" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/fc8c894f-872a-42e7-b144-14c335883228">
<img width="626" alt="Capture4" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/f1b1b143-7b4a-48e6-b156-a2289e819632">
<img width="665" alt="Capture5" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/f1d19b3b-f8be-4486-b5d0-c0cd974e47eb">
<img width="657" alt="Capture6" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/52ecd591-b013-4efd-ab48-35e02b3f33d4">
<img width="659" alt="Capture7" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/452f36ab-80de-44e8-8eb9-4bae2190b0ae">
<img width="689" alt="Capture8" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/3f576437-3c44-405d-bf71-0ec8f317a65b">
<img width="825" alt="Capture9" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/8416b47e-5154-45fe-8328-18ce13f958e2">
<img width="427" alt="Capture10" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/e44b0733-d74d-4a65-814c-0ff480044970">
<img width="948" alt="Capture11" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/a60e79d7-f330-40b7-819f-bf22a04f2de1">
<img width="954" alt="Capture12" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/6a071c5e-8f2c-4a88-9e2d-dbf0b91e9653">
<img width="387" alt="Capture13" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/67b5bf9a-f2a0-4fd1-84bf-1b1f10e861c8">
<img width="426" alt="Capture14" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/2fda3cdd-32ec-4105-93e9-e6aced0c763f">
<img width="422" alt="Capture15" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/fec36c90-1cec-466d-a5c7-34e5d5d286ac">


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

