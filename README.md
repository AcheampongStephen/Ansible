# Ansible Installation Guide for Ubuntu

## Step 1: Update Package Lists
### Update the Package Manager:
Open your Ubuntu terminal and run:
```bash
sudo apt update
sudo apt upgrade -y
```
This updates and upgrades the list of available packages and their versions.

## Step 2: Install Required Packages
### Install Software Properties:
Install the `software-properties-common` package:
```bash
sudo apt install software-properties-common
```

## Step 3: Add Ansible PPA (Personal Package Archive)
### Add the Ansible Repository:
Run the following command to add the Ansible repository:
```bash
sudo add-apt-repository --yes --update ppa:ansible/ansible
```

## Step 4: Install Ansible
### Install Ansible:
Now, install Ansible with:
```bash
sudo apt install ansible -y
```

## Step 5: Verify Installation
### Check Ansible Version:
To confirm that Ansible is installed correctly, run:
```bash
ansible --version
```

