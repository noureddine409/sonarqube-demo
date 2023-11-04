# Installation de SonarQube dans Azure VM

Ce guide vous guidera à travers le processus de création d'une machine virtuelle (VM) Azure et de l'installation de SonarQube dessus. SonarQube est une plateforme open source qui vous permet d'inspecter en continu et d'améliorer la qualité de votre code.

## Prérequis

1. Compte Azure : Vous aurez besoin d'un compte Azure actif pour créer une machine virtuelle.
2. Une compréhension de base des services Azure et des machines virtuelles.

## Step 1: Create an Azure VM
<img width="960" alt="Capture" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/b7a95024-6e5e-4b7f-a61c-757195b7cb74">
<img width="523" alt="Capture2" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/e161973f-c99d-4610-bdb3-9365481c9e76">
<img width="627" alt="Capture3" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/ccb2611d-5a5b-4268-9def-b59b83df037d">
<img width="626" alt="Capture4" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/612b2ab5-fab2-4ddb-9a85-bb8bf9cda458">

<img width="665" alt="Capture5" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/ee67442d-4ed6-4d8e-becc-f6b3b19e00db">
<img width="657" alt="Capture6" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/50a6dfe3-6d8f-4450-928d-3e4902b86f4e">
<img width="659" alt="Capture7" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/bb00bb90-c5f4-41cd-82d7-5298a2c3ea15">

<img width="689" alt="Capture8" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/0dddfa5b-3b50-46b8-bf86-6682f3a96177">
<img width="825" alt="Capture9" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/f4d16dce-75a6-47bb-8dce-b94a8982127d">
<img width="427" alt="Capture10" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/bc1c7a5d-c812-449b-8e96-e759063401e6">
<img width="948" alt="Capture11" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/a500b045-d1d1-48a8-874c-2dc54c8509bb">
<img width="954" alt="Capture12" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/118e09d8-a4f7-487a-9d7c-6c01ed454f0b">
<img width="387" alt="Capture13" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/04e2c99f-0a5a-43d9-a364-282ae4d96e4f">
<img width="426" alt="Capture14" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/2c5de9b2-e353-40c1-8fb6-8ab26529ecb1">
<img width="422" alt="Capture15" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/2fa932c7-648c-4a04-8ba5-58018ba9ef01">

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
