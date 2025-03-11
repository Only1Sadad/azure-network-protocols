# **Azure Virtual Machines & Network Traffic Lab Guide**  

## **Part 1: Creating Virtual Machines**  
📍 **Azure Portal:** [https://portal.azure.com/](https://portal.azure.com/)  

### **Step 1: Create a Resource Group**  
- Navigate to **Azure Portal → Resource Groups**  
- Click **Create a new Resource Group**  
- Name it appropriately (e.g., "Lab-RG")  

### **Step 2: Create a Windows 10 Virtual Machine (VM)**  
- Navigate to **Virtual Machines → Create a new VM**  
- Select the previously created **Resource Group**  
- Allow Azure to **create a new Virtual Network (VNet) and Subnet**  
- Configure authentication as **Username/Password**  
- Deploy the VM  

### **Step 3: Create a Linux (Ubuntu) Virtual Machine (VM)**  
- Navigate to **Virtual Machines → Create a new VM**  
- Select the **same Resource Group** and **same Virtual Network** created earlier  
- Configure authentication as **Username/Password**  
- Ensure both VMs are in the **same VNet and Subnet**  
- Deploy the VM  

🛑 **End of Part 1:** Keep both VMs running for **Part 2**  

---

## **Part 2: Observing ICMP Traffic**  
📍 **Azure Portal:** [https://portal.azure.com/](https://portal.azure.com/)  

### **Step 1: Set Up Remote Desktop**  
- **Windows:** Use built-in **Remote Desktop Connection**  
- **Mac:** Install **Microsoft Remote Desktop**  
- Connect to your **Windows 10 VM** using **RDP**  

### **Step 2: Install & Use Wireshark**  
- Within the Windows 10 VM, **install Wireshark**  
- Open Wireshark and **start a packet capture**  
- **Filter for ICMP traffic** (ping traffic)  

### **Step 3: Test ICMP (Ping) Traffic**  
1. **Find the Private IP of the Ubuntu VM**  
   - Go to **Azure Portal → Virtual Machines → Ubuntu VM → Networking**  
   - Note the **private IP address**  
2. **Ping the Ubuntu VM from Windows 10 VM**  
   - Open **Command Prompt (cmd.exe) or PowerShell**  
   - Run: `ping <Ubuntu Private IP>`  
   - Observe **ICMP requests/replies** in **Wireshark**  
3. **Ping a Public Website**  
   - In **Windows 10 VM**, run:  
     ```powershell
     ping www.google.com
     ```  
   - Observe **outgoing ICMP traffic** in Wireshark  

---

## **Part 3: Configuring Firewall (Network Security Group) & Observing Traffic**  

### **Step 1: Block ICMP Traffic**  
1. **Initiate a nonstop ping**  
   ```powershell
   ping <Ubuntu Private IP> -t
