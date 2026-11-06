# A Beginner-Friendly Tutorial on How to Install an ARO Network Linux Server Node

This guide walks beginners through installing and checking an **ARO Network Server Node** on **Debian 13**.

The instructions focus on the ARO **Server Node** package. This is different from ARO Desktop, ARO Mobile, and ARO Lite.

> **Note:** This is a community-written guide. ARO Network's official documentation remains the source of truth for installation requirements and updates. Always check the official guide if an installation step changes.

## Table of Contents

- [1. What You Need](#1-what-you-need)
- [2. Install Debian 13](#2-install-debian-13)
- [3. Prepare Debian](#3-prepare-debian)
- [4. Install the ARO Server Node](#4-install-the-aro-server-node)
- [5. Check That the Node Is Running](#5-check-that-the-node-is-running)
- [6. Connect to the ARO Dashboard](#6-connect-to-the-aro-dashboard)
- [7. Useful Commands](#7-useful-commands)
- [8. Troubleshooting](#8-troubleshooting)
- [9. Official Resources](#9-official-resources)

## 1. What You Need

Before you begin, make sure you have:

- A computer running Debian 13 (64-bit)
- An active and stable internet connection
- Administrator access to the Debian system
- A working terminal
- A physical computer for the DEB installation procedure described in the current official installation guide

**Important:** The official ARO Server DEB installation guide specifies Debian 11 or later and root access. It also warns that this installation procedure will fail in a virtual machine. Check the official documentation for the latest compatibility requirements before proceeding.

## 2. Install Debian 13

If Debian 13 is not yet installed on your computer, follow this video tutorial first:

**[Watch: Debian 13 Installation Tutorial](https://youtu.be/PAWzoDgVgyY?si=gfKclgjcxKOjSUlo)**

Complete the Debian installation and connect your computer to the internet.

> This guide assumes Debian 13 is already installed and that you can log in and open the terminal.

## 3. Prepare Debian

Open the Terminal.

First, update the package list and install available updates:

```bash
sudo apt update
sudo apt upgrade -y
```

Enter your password if prompted.

Next, switch to the root account:

```bash
sudo -i
```

Your terminal prompt should now indicate that you are logged in as root. The remaining installation commands in this guide are run as root.

## 4. Install the ARO Server Node

Update the package list as root:

```bash
apt update
```

Download the official ARO Server DEB package:

```bash
wget -O /tmp/aro-client-1.0.0.deb https://download.aro.network/files/deb/aro-client-1.0.0.deb
```

Install the package:

```bash
apt install -f /tmp/aro-client-1.0.0.deb
```

If the installer asks you to confirm, type `Y` and press **Enter**.

Wait for the installation to finish. Do not close the terminal while the installation is running.

When installation is complete, you can leave the root shell:

```bash
exit
```

## 5. Check That the Node Is Running

Check the ARO agent service:

```bash
sudo systemctl status agent --no-pager
```

Look for **Active: active (running)** in the output.

To watch the live service logs:

```bash
sudo journalctl -u agent -f
```

Press **Ctrl + C** to stop viewing the live logs. This does not stop the ARO service.

If the service name is different on your installation, list ARO-related services with:

```bash
systemctl list-units --type=service --all | grep -i aro
```

## 6. Connect to the ARO Dashboard

The ARO Dashboard is used to manage your ARO nodes and view your Jade rewards.

1. Open the [ARO Dashboard](https://dashboard.aro.network/).
2. Create an ARO account or sign in to your existing account.
3. Open the **ARO Node** section to view nodes linked to your account.
4. To add a Server Node, use **Add New Node** and select the **ARO Server** option if it is shown.
5. Follow the Server-specific setup instructions displayed by the Dashboard.

**Important:** The ARO Desktop, ARO Lite, and ARO Mobile guides describe their own Serial Number (SN) binding processes. Do not use those instructions or assume their SN commands apply to the ARO Server package. Follow the ARO Server flow shown in the Dashboard and its official installation guide.

This community guide currently documents the Debian package installation and Linux service checks. The exact Server Node account-binding or SN retrieval steps should be added only after they have been verified on a real ARO Server installation.

## 7. Useful Commands

| Task | Command |
| --- | --- |
| Check agent status | `sudo systemctl status agent --no-pager` |
| Restart the agent | `sudo systemctl restart agent` |
| View live agent logs | `sudo journalctl -u agent -f` |
| List ARO-related services | `systemctl list-units --type=service --all \| grep -i aro` |
| Check installed ARO package | `dpkg -l \| grep -i aro` |

## 8. Troubleshooting

### The installation says root access is required

Switch to the root account before running the installation commands:

```bash
sudo -i
```

### The node appears offline after Debian goes to sleep

Check Debian's power and sleep settings. The computer must remain awake and connected to the internet for the node to stay online.

### The dashboard reports an outdated agent version

Make sure the computer has an internet connection and allow time for the agent's automatic update. If the warning remains, consult ARO support.

### The agent service is not running

Check its status and logs:

```bash
sudo systemctl status agent --no-pager
sudo journalctl -u agent -n 100 --no-pager
```

### The node cannot connect to the ARO network

Check your firewall and router settings against the port requirements in the official [ARO Server FAQ & Troubleshooting](https://docs.aro.network/node-operator-guide/aro-server/aro-server-faq-troubleshooting/). Do not open ports unless you understand your network's security settings.

## 9. Official Resources

- [ARO Server Installation Guide](https://docs.aro.network/node-operator-guide/aro-server/aro-server-installation-guide/)
- [ARO Server FAQ & Troubleshooting](https://docs.aro.network/node-operator-guide/aro-server/aro-server-faq-troubleshooting/)
- [ARO Dashboard Guide](https://docs.aro.network/node-operator-guide/become-operator/aro-dashboard/)
- [ARO Network Website](https://aro.network/)
- [Debian 13 Installation Video](https://youtu.be/PAWzoDgVgyY?si=gfKclgjcxKOjSUlo)

---

**Tutorial platform:** Debian 13  
**Node type:** ARO Network Server Node  
**Maintained by:** AXES-SPEC

If you find an instruction that no longer works, please open an issue so the guide can be reviewed and updated.
