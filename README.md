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

# Ansible Control Node Setup on Ubuntu (EC2 Instance)

If you are using an **EC2 instance** as the control node, follow these steps to configure **SSH access** to the Ansible host.

## 1️⃣ Generate SSH Key Pair on the Control Node
1. Navigate to the `.ssh` directory:
   ```bash
   cd ~/.ssh
   ```
2. List existing SSH keys:
   ```bash
   ls
   ```
3. Generate a new SSH key pair:
   ```bash
   ssh-keygen
   ```
   - Press **Enter** for all prompts to accept defaults.

4. Verify the key has been created:
   ```bash
   ls
   ```

5. Copy the generated public key:
   ```bash
   cat id_rsa.pub
   ```

## 2️⃣ Configure SSH Access on the Worker Node
1. SSH into the **worker node**:
   ```bash
   ssh ubuntu@<worker-node-ip>
   ```
2. Install Python (if not already installed):
   ```bash
   sudo apt update && sudo apt install -y python3
   ```
3. Navigate to the `.ssh` directory:
   ```bash
   cd ~/.ssh
   ```
4. Open the `authorized_keys` file for editing:
   ```bash
   nano authorized_keys
   ```
5. Paste the copied public key (`id_rsa.pub`) from the **control node** into this file.
6. Save and exit (**CTRL + X**, then **Y**, then **Enter**).

## 3️⃣ Test SSH Connection
On your **control node**, test SSH access:
```bash
ssh ubuntu@<worker-node-ip>
```
You should be able to securely SSH into the worker node **without password authentication**.

---

Now your **control node** is ready to manage the **worker node** using Ansible! 🚀



### Using Password 

- Go to the file `/etc/ssh/sshd_config.d/60-cloudimg-settings.conf`
- Update `PasswordAuthentication yes`
- Restart SSH -> `sudo systemctl restart ssh`

