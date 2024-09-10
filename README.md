# Day-7-Setting-Up-Elastic-Fleet-Server-and-Enrolling-Windows-Server

Managing multiple servers and keeping track of their logs, metrics, and overall health is crucial for IT professionals. The Elastic Stack offers a powerful solution with its Elastic Agent and Fleet Server. In this guide, we’ll walk you through the steps to create a Fleet Server, install an Elastic Agent on a Windows Server, and enroll that server into the fleet for centralized monitoring.

## Objectives
- Install Elastic Agent on a Windows Server.
- Enroll the Windows Server into a Fleet.

## Step 1: Create a Fleet Server on Vultr

To begin, we need to set up a Fleet Server that will manage the Elastic Agents.

### 1.1 Deploy a Fleet Server on Vultr

1. Go to [Vultr](https://vultr.com) and click the **Deploy** button to create a new server.
2. Select **Optimized Cloud Compute — Dedicated CPU** as the type.
3. Choose a location of your preference.
4. Under the image section, select **Ubuntu 22.04 LTS**.
5. For the plan, select **30 GB NVMe, 1 CPU, 4 GB Memory**. This configuration should be sufficient for our needs.
6. Once everything is set up, click **Deploy** to launch the server.

### 1.2 Access the Elastic GUI and Configure Fleet

1. Open your Elastic GUI and click the **hamburger icon** on the left-hand side.
2. Scroll down to the **Management** tab and select **Fleet**.
3. Click **Add Fleet Server**. You will see two options: **Quick Start** and **Advanced**. For this guide, we’ll use **Quick Start**. If you are setting up in a production environment, consider using the **Advanced** option for more granular control.
4. Enter a name for your Fleet Server.
5. For the URL, use the public IP address of the Fleet Server created on Vultr in the previous step.
6. Elastic will generate a Fleet Service Policy and a Service Token. **Copy these** as they are needed for the next steps.

## Step 2: Install Fleet Server on Ubuntu

### 2.1 SSH into the Fleet Server

1. Open your terminal and SSH into your Fleet Server using the command:

    ```bash
    ssh root@<Your_Fleet_Server_Public_IP>
    ```

2. Once connected, update and upgrade the repositories:

    ```bash
    apt-get update && apt-get upgrade
    ```

3. After upgrading, paste the installation command provided by the Elastic GUI into the terminal. This command will install the Elastic Agent and configure it to connect to the Elastic Stack using the Service Policy and Token.

### 2.2 Configure Firewall Rules

1. In your Vultr dashboard, update the firewall rules for the Fleet Server to allow access to the necessary ports.
2. On the Fleet Server, allow traffic on port 9200:

    ```bash
    ufw allow 9200
    ```

3. After successful enrollment, check the Elastic GUI to confirm the Fleet Server is connected. The Fleet Server should now be visible under the **Fleet** tab in the Elastic GUI.

![insert image here](image.jpg)
### Successfully Installed Elastic Agent in Fleet Server

## Step 3: Enroll a Windows Server into Fleet

Now that our Fleet Server is up and running, we can install an Elastic Agent on a Windows Server and enroll it into the fleet.

### 3.1 Install Elastic Agent on Windows Server

1. Go back to the Elastic GUI and click **Add Agent** again.
2. Provide a name for your Windows Server to create a new policy. Choose options for collecting system logs and metrics, and click **Create Policy**.
3. An installation command will be generated. **Copy this command**.

### 3.2 Execute the Installation Command on Windows Server

1. On your Windows Server, open PowerShell with administrative privileges.
2. Paste the installation command you copied from the Elastic GUI and run it.
3. Go back to your Fleet Server and allow traffic on port 8200:

    ```bash
    ufw allow 8200
    ```

4. Once the Elastic Agent is successfully installed, the Windows Server will appear under the **Fleet Management** tab in the Elastic GUI.

![insert image here](image.jpg)
### Successfully Installed Fleet in Windows Server

### 3.3 Verify the Enrollment

1. Head over to the **Discover** tab in the Elastic GUI.
2. Type your Windows Server name to search for its logs.
3. You should now see logs and metrics related to your Windows Server, indicating successful enrollment and data collection.

![insert image here](image.jpg)
## Conclusion

In this guide, we successfully created a new Fleet Server using Vultr, installed the Elastic Agent on a Windows Server, and enrolled it into our fleet. This setup will allow you to monitor and manage your servers centrally, giving you real-time insights into their health and performance.
