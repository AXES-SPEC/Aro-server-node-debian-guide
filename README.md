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
- [6. Connect the Server to the ARO Dashboard](#6-connect-the-server-to-the-aro-dashboard)
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

Update the package list and install available updates:

```bash
sudo apt update
sudo apt upgrade -y
```

Enter your password if prompted.

## 4. Install the ARO Server Node

Download the official ARO Server DEB package:

```bash
wget -O /tmp/aro-client-1.0.0.deb https://download.aro.network/files/deb/aro-client-1.0.0.deb
```

Install the package using administrator privileges:

```bash
sudo apt install -f /tmp/aro-client-1.0.0.deb
```

If the installer asks you to confirm, type `Y` and press **Enter**.

Wait for the installation to finish. Do not close the terminal while the installation is running.

**Important:** Do not run `apt install` without `sudo` or root access. If you see a message saying it cannot open the dpkg lock or asks whether you are root, repeat the installation command with `sudo`.

If the installer reports that `aro` is already the newest version, the package is already installed. Continue to the service check below.

## 5. Check That the Node Is Running

Check the ARO agent service:

```bash
sudo systemctl status agent --no-pager
```

Look for **Active: active (running)** in the output. This confirms that the agent service is running on your computer.

To watch the live service logs:

```bash
sudo journalctl -u agent -f
```

Press **Ctrl + C** to stop viewing the live logs. This does not stop the ARO service.

If the service name is different on your installation, list ARO-related services with:

```bash
systemctl list-units --type=service --all | grep -i aro
```

## 6. Connect the Server to the ARO Dashboard

After confirming that the ARO agent is running, link your server to your ARO account.

1. Open the [ARO Dashboard](https://dashboard.aro.network/).
2. Sign in to your account.
3. Select **ARO Nodes**.
4. Select **Add New Node**, then choose **Server**.
5. The page displays **Step 1: Connect your device** and asks for the device's Serial Number (SN).
6. On the Debian computer running the ARO Server Node, run:

```bash
sudo cat /etc/enreach/x86_sn
```

7. Copy the Serial Number shown in the terminal.
8. Paste it into the Serial Number field on the Dashboard and select **Continue**.
9. Follow any remaining instructions displayed by the Dashboard to complete linking.

**Keep your Serial Number private.** Do not post it in public screenshots, GitHub issues, Discord, or social media. Redact the value before sharing terminal screenshots.

If the file does not exist on your installation, do not guess another Serial Number. Check the official [ARO Server Installation Guide](https://docs.aro.network/node-operator-guide/aro-server/aro-server-installation-guide/) or contact ARO support for the current method.

> The Serial Number command above is for the ARO Server setup described in this guide. Do not substitute instructions for ARO Desktop, ARO Lite, or ARO Mobile.

## 7. Useful Commands

| Task | Command |
| --- | --- |
| Update Debian package list | `sudo apt update` |
| Install or repair ARO package | `sudo apt install -f /tmp/aro-client-1.0.0.deb` |
| Check agent status | `sudo systemctl status agent --no-pager` |
| Restart the agent | `sudo systemctl restart agent` |
| View live agent logs | `sudo journalctl -u agent -f` |
| Read the Server Serial Number | `sudo cat /etc/enreach/x86_sn` |
| Check installed ARO package | `dpkg -l | grep -i aro` |

## 8. Troubleshooting

### The installation says root access is required

Use `sudo` before the package installation command:

```bash
sudo apt install -f /tmp/aro-client-1.0.0.deb
```

### The package is already installed

If APT reports that `aro` is already the newest version, do not reinstall it unnecessarily. Check the service:

```bash
sudo systemctl status agent --no-pager
```

### The node appears offline after Debian goes to sleep

Check Debian's power and sleep settings. The computer must remain awake and connected to the internet for the node to stay online.

### The dashboard reports an outdated agent version

Make sure the computer has an internet connection and allow time for the agent's automatic update. If the warning remains, consult ARO support.

### The agent service is not running

Check its status and recent logs:

```bash
sudo systemctl status agent --no-pager
sudo journalctl -u agent -n 100 --no-pager
```

### The Serial Number file cannot be found

Check the official ARO Server documentation or contact ARO support. Do not enter a Serial Number from another device.

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
