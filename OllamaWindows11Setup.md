# Ollama Windows 11 Setup

## 1. Download and Install Ollama

1. Download the latest Ollama installer from the official website:
   - [Ollama Windows Installer](https://ollama.com/download/OllamaSetup.exe)

2. Run `OllamaSetup.exe` and follow the on-screen installation instructions.

## 2. Set Environment Variable

To allow external access, set the `OLLAMA_HOST` environment variable:

1. Open **Command Prompt** as Administrator.
2. Run the following command:
   ```cmd
   setx OLLAMA_HOST "0.0.0.0" /M
   ```
3. Restart your computer for the changes to take effect.

## 3. Open Firewall Port 11434

To allow incoming connections to Ollama, open port `11434` in Windows Firewall:

1. Open **PowerShell** as Administrator.
2. Run the following command:
   ```powershell
   New-NetFirewallRule -DisplayName "Allow Ollama" -Direction Inbound -Protocol TCP -LocalPort 11434 -Action Allow
   ```

## 4. Verify Installation

After installation, verify that Ollama is running:

1. Open **Command Prompt** and run:
   ```cmd
   ollama run llama2
   ```
   This should start an Ollama model if the installation was successful.

2. Check if the server is accessible:
   ```cmd
   curl http://localhost:11434
   ```
   If the installation was successful, you should see a response from the Ollama API.

## 5. Additional Setup (Optional)

If you need to **start Ollama on boot**, create a startup task:

```powershell
schtasks /create /tn "Ollama Startup" /tr "C:\\Program Files\\Ollama\\ollama.exe serve" /sc onlogon /rl highest
```

## Mac & Linux Installation

For **Mac** and **Linux** installation, follow the official Ollama guides:

- **Mac**: [Ollama for macOS](https://ollama.com)
- **Linux**: [Ollama for Linux](https://ollama.com)

---
Now your **Ollama server** is installed, configured, and accessible over the network!
