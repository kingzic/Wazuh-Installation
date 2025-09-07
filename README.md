 **Wazuh Installation on Ubuntu Machine** 

---

````markdown
#  How to Setup Wazuh on Ubuntu

This guide explains how to install and troubleshoot Wazuh on an Ubuntu machine.

---

##  Prerequisites
- Installed Ubuntu (e.g., on VirtualBox).
- Ensure you have `curl` installed:

```bash
sudo apt install curl
````

---

##  Initial Attempt and Errors

### Adding Wazuh GPG Key

```bash
curl -sO https://packages.wazuh.com/4.x/wazuh-repository.key && \
sudo gpg --no-default-keyring --keyring /usr/share/keyrings/wazuh-archive-keyring.gpg --import ./wazuh-repository.key
```

Error: `no default keyring`

---

### Adding Wazuh Repository

```bash
echo "deb [signed-by=/usr/share/keyrings/wazu-archive-keyring.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list
```

 Error: `no file or directory`

---

##  Removing Previous Wazuh Installations

To clean up and start fresh, remove all Wazuh components:

```bash
sudo systemctl stop wazuh-dashboard
sudo apt-get purge wazuh-dashboard

sudo systemctl stop wazuh-manager
sudo apt-get purge wazuh-manager
sudo rm -rf /var/ossec
sudo rm -rf /etc/filebeat

sudo systemctl stop wazuh-indexer
sudo apt-get purge wazuh-indexer
sudo rm -rf /var/lib/wazuh-indexer
sudo rm -rf /var/log/wazuh-indexer

sudo apt-get purge opensearch opensearch-dashboards filebeat
sudo rm -rf /etc/apt/sources.list.d/wazuh.list

sudo apt-get update
```

---

##  Correct Installation Steps

### Step 1: Run Wazuh Installer

For **Wazuh 4.7**:

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
```

 Note: Wazuh **4.7** is only compatible with **Ubuntu 22.04 and lower**.

---

For **Ubuntu 24.04**, use **Wazuh 4.12**:

```bash
curl -sO https://packages.wazuh.com/4.12/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
```

---

### Step 2: Hardware Requirements

If you get an error about minimum hardware requirements, adjust **VirtualBox settings**:

* **Base Memory**: 4 GB (minimum)
* **Processors**: 2 CPU cores

---

### Step 3: Final Run

Re-run the installer:

```bash
curl -sO https://packages.wazuh.com/4.12/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
```

 This will generate your **Wazuh username and password**.

---

##  Accessing Wazuh

Login with the provided credentials after installation completes.

---


