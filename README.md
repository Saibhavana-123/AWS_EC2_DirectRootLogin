# AWS EC2 Direct Root Login via SSH

A step-by-step practical demonstrating how to configure and test direct root login to an Ubuntu Amazon EC2 instance using SSH password authentication through MobaXterm in an AWS Academy Sandbox.

## Project Overview

This practical covers launching or accessing an Ubuntu EC2 instance, connecting through SSH, setting a root password, modifying SSH server configuration, and verifying root login.

**Note:** Direct root login using an SSH password is intended only for a controlled lab demonstration and is not recommended for production environments.

## Objectives

- Start the AWS Academy Sandbox.
- Launch or access an Ubuntu EC2 instance.
- Configure SSH connectivity through MobaXterm.
- Set a password for the root account.
- Configure SSH authentication for the lab demonstration.
- Test and verify direct root login.
- Restore safer SSH settings after testing.

## Tools and Technologies

| Tool / Technology | Purpose |
|---|---|
| AWS Academy Sandbox | Provides a temporary AWS lab environment |
| Amazon EC2 | Hosts the virtual machine |
| Ubuntu Server | Operating system |
| MobaXterm | SSH client for remote access |
| OpenSSH | SSH server and authentication configuration |
| Linux Terminal | Executes administrative commands |

## Prerequisites

- Access to an AWS Academy Sandbox.
- A running Ubuntu EC2 instance.
- The instance's public IPv4 address or public DNS name.
- MobaXterm installed on Windows.
- The SSH private key associated with the instance.
- SSH access allowed on TCP port `22` from an approved IP address.
- An Ubuntu account with `sudo` privileges.

## Implementation Steps

### 1. Start AWS Academy Sandbox

1. Open the AWS Academy course.
2. Navigate to **Modules → Sandbox Environment**.
3. Start the lab and wait until it is ready.
4. Open the AWS Management Console.

### 2. Launch or Select an EC2 Instance

1. Open the EC2 service.
2. Select **Instances**.
3. Launch an Ubuntu instance if required and permitted by the lab.
4. Wait until the instance reaches the **Running** state.
5. Note its public IPv4 address and security group.

### 3. Connect Through MobaXterm

1. Open MobaXterm.
2. Select **Session → SSH**.
3. Enter the EC2 public IP address.
4. Use `ubuntu` as the username for a standard Ubuntu EC2 image.
5. Select the corresponding SSH private key.
6. Connect and verify the account:

```bash
whoami
hostname
id
```

### 4. Configure SSH

Open the SSH server configuration file:

```bash
sudo nano /etc/ssh/sshd_config
```

For the temporary lab demonstration, the practical uses these settings:

```text
PermitRootLogin yes
PubkeyAuthentication no
PasswordAuthentication yes
KbdInteractiveAuthentication yes
```

Save the file and exit Nano.

### 5. Set the Root Password

Run:

```bash
sudo passwd root
```

Enter a strong, unique lab password when prompted. Do not include the password in screenshots or commit it to GitHub.

### 6. Validate and Restart SSH

Check the configuration:

```bash
sudo sshd -t
```

If no errors are reported, restart the SSH service:

```bash
sudo systemctl restart ssh
```

### 7. Test Direct Root Login

Create a new SSH session in MobaXterm using the username `root`. Enter the root password when prompted.

After successful login, verify the account:

```bash
whoami
id
```

A successful root session should show `root` and UID `0`.

### 8. Restore Safer SSH Settings

After the demonstration, restore the original configuration or a safer policy. A common baseline is:

```text
PermitRootLogin
