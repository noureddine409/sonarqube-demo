# Installation de SonarQube dans Azure VM

Ce guide vous guidera à travers le processus de création d'une machine virtuelle (VM) Azure et de l'installation de SonarQube dessus. SonarQube est une plateforme open source qui vous permet d'inspecter en continu et d'améliorer la qualité de votre code.

## Prérequis

1. Compte Azure : Vous aurez besoin d'un compte Azure actif pour créer une machine virtuelle.
2. Une compréhension de base des services Azure et des machines virtuelles.

## Step 1: Creation de Azure VM
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

## :warning: Attention : Arrêtez votre machine virtuelle Azure après que vous avez terminé.

Azure facture l'utilisation des machines virtuelles en cours d'exécution. Veuillez vous assurer d'arrêter votre machine virtuelle Azure lorsque vous avez terminé pour éviter des frais inutiles.

## Connecter a votre azure VM utilisant ssh

1. Ouvrez un terminal sur votre ordinateur local.

2. Utilisez la commande suivante pour sécuriser votre fichier PEM que vous avez conservé après la création de votre machine virtuelle Azure. Assurez-vous que seuls vous et l'administrateur pouvez le lire. Remplacez votre-clé.pem par le nom de votre fichier PEM 

   ```sh
   chmod 600 sonarqube-server_key.pem.pem
   ```

3. Connectez-vous à la machine virtuelle en utilisant la commande ssh. Remplacez votre-clé.pem, adresse-IP, et utilisateur par les valeurs appropriées.

   ```sh
   ssh -i chemin-vers-la-clé/sonarqube-server_key.pem azureuser@Address-IP-Public
   ```

   vous trouver l'adress ip public ici

<img width="941" alt="aa" src="https://github.com/noureddine409/sonarqube-demo/assets/83149531/618f1ed1-75d8-4bd4-ae0b-476db20950ff">

## Installer Sonarqube
1. Mettez à jour votre liste de packages et mettez à niveau les packages existants.

```sh
# Update your package list and upgrade existing packages
sudo apt update
sudo apt upgrade
```
2. installer java runtime environment et unzip

  ```sh
sudo apt install default-jre
java -version
sudo apt install unzip
```

3. installer et configurer sonarqube

  ```sh
adduser sonarqube
sudo su - sonarqube
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.4.0.54424.zip
unzip *
chmod -R 755 /home/sonarqube/sonarqube-9.4.0.54424
chown -R sonarqube:sonarqube /home/sonarqube/sonarqube-9.4.0.54424
cd sonarqube-9.4.0.54424/bin/linux-x86-64/
./sonar.sh start
```


Vous pouvez désormais accéder au serveur SonarQube sur http://<adresse-ip>:9000.

