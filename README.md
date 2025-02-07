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

# How to setup Passwordless Authentication

## EC2 Instances

### Using Public Key

```
ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP>
```

- ssh-copy-id: This is the command used to copy your public key to a remote machine.
- -f: This flag forces the copying of keys, which can be useful if you have keys already set up and want to overwrite them.
- "-o IdentityFile <PATH TO PEM FILE>": This option specifies the identity file (private key) to use for the connection. The -o flag passes this option to the underlying ssh command.
- ubuntu@<INSTANCE-IP>: This is the username (ubuntu) and the IP address of the remote server you want to access.

### Using Password 

- Go to the file `/etc/ssh/sshd_config.d/60-cloudimg-settings.conf`
- Update `PasswordAuthentication yes`
- Restart SSH -> `sudo systemctl restart ssh`

