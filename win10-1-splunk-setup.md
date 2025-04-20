# 🧠 Splunk Forwarder Setup (Win10-1)

This endpoint uses the Splunk Universal Forwarder to send logs to the local Splunk instance.

## 🔧 Setup Steps

1. Downloaded Splunk UF from [splunk.com](https://www.splunk.com/en_us/download/universal-forwarder.html)
2. Installed with:
   - Logon as `Local System`
   - Forwarded to `localhost:9997`
3. Configured inputs:
   - Sysmon logs
   - Windows Event Logs (Security, PowerShell, Sysmon)

## 📂 Example inputs.conf

```conf
[WinEventLog://Microsoft-Windows-Sysmon/Operational]
disabled = 0

[WinEventLog://Security]
disabled = 0

[WinEventLog://Windows PowerShell]
disabled = 0
