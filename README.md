Here’s a more engaging version of the repository using emojis to highlight key components and maintaining all the links and commands:

# 🌟 Day-7: Setting Up Elastic Fleet Server and Enrolling Windows Server 🌟

Managing multiple servers and tracking logs, metrics, and overall health is crucial for IT professionals. With Elastic Stack's **Elastic Agent** and **Fleet Server**, this becomes a breeze! 💨 In this guide, we'll walk through setting up a Fleet Server, installing Elastic Agent on a Windows Server, and enrolling the server into the fleet for centralized monitoring. 🖥️

## 🎯 Objectives:
- Install Elastic Agent on a Windows Server 🖥️
- Enroll the Windows Server into a Fleet 🚀

---

## 🛠️ Step 1: Create a Fleet Server on Vultr

We’ll start by setting up a **Fleet Server** to manage the Elastic Agents.

### 1.1 🚀 Deploy a Fleet Server on Vultr

1. Go to [Vultr](https://vultr.com) and click the **Deploy** button.
2. Select **Optimized Cloud Compute — Dedicated CPU** for the server type ⚙️.
3. Choose a location 🌍 of your choice.
4. Under **Image**, select **Ubuntu 22.04 LTS** 🐧.
5. Pick the **30 GB NVMe, 1 CPU, 4 GB Memory** plan 💾—this is perfect for our setup!
6. Click **Deploy** to launch your server 🎉.

---

### 1.2 🔧 Access the Elastic GUI and Configure Fleet

1. Open the **Elastic GUI** and click the **hamburger icon** (☰) on the left.
2. Scroll to **Management** and select **Fleet**.
3. Click **Add Fleet Server**. Choose **Quick Start** for simplicity. If you’re working in production, you may want to consider the **Advanced** option for more control ⚙️.
4. Enter a name for your **Fleet Server**.
5. Use the public IP of the Fleet Server you just created on Vultr 🌐.
6. **Copy** the Fleet Service Policy and Service Token — you'll need these later 📋.

---

## 🖥️ Step 2: Install Fleet Server on Ubuntu

### 2.1 💻 SSH into the Fleet Server

1. Open your terminal and SSH into your Fleet Server using:

   ```bash
   ssh root@<Your_Fleet_Server_Public_IP>
   ```

2. Update and upgrade your server’s packages 💡:

   ```bash
   apt-get update && apt-get upgrade
   ```

3. Now, paste the **installation command** from the Elastic GUI into the terminal. This installs the **Elastic Agent** and configures it to connect to the Elastic Stack 🚀.

---

### 2.2 🔐 Configure Firewall Rules

1. In your Vultr dashboard, update the firewall rules to allow access to the Fleet Server 🔒.
2. Allow traffic on port **9200** on the Fleet Server by running:

   ```bash
   ufw allow 9200
   ```

3. Check the **Elastic GUI** to confirm your Fleet Server is connected ✅. It should now be visible under the **Fleet** tab in the Elastic GUI.

![Fleet Server Connected](image.jpg)  
*Your Fleet Server should now be successfully installed and connected!*

---

## 🛠️ Step 3: Enroll a Windows Server into Fleet

Now that the Fleet Server is up, let’s install the Elastic Agent on your **Windows Server** and enroll it in the fleet for monitoring 🛡️.

### 3.1 📦 Install Elastic Agent on Windows Server

1. In the **Elastic GUI**, click **Add Agent**.
2. Name your Windows Server and create a new policy to collect logs and metrics 📊.
3. Copy the **installation command** provided by the Elastic GUI.

---

### 3.2 💻 Run the Installation Command on Windows Server

1. On your Windows Server, open **PowerShell** as an administrator ⚙️.
2. Paste the **installation command** from the Elastic GUI and execute it.
3. Allow traffic on port **8200** on your Fleet Server by running:

   ```bash
   ufw allow 8200
   ```

4. After installing the Elastic Agent, the Windows Server will appear in the **Fleet Management** tab 🖥️.

![Windows Server Enrolled](image.jpg)  
*Windows Server successfully enrolled!*

---

### 3.3 🔍 Verify the Enrollment

1. Go to **Discover** in the Elastic GUI 🔍.
2. Search for your Windows Server name to check its logs 📈.
3. You should now see logs and metrics, confirming successful enrollment and data collection! 💪

![Windows Server Logs](image.jpg)  
*Logs and metrics successfully flowing!*

---

## 🎉 Conclusion

Congratulations! 🎊 You've successfully created a **Fleet Server** on Vultr, installed the **Elastic Agent** on a **Windows Server**, and enrolled it into the fleet. With this setup, you can now monitor and manage all your servers from a central dashboard, getting real-time insights into their health and performance 🛡️🚀.

Keep monitoring and stay secure! 🔐
