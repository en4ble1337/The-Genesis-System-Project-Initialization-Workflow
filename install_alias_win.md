## Windows Installation

On Windows, the native equivalent of a shell alias is a PowerShell Function added to your user profile.

### Step 1: Install the Command

Copy the entire block below, paste it into PowerShell, and press Enter. This script automatically finds your PowerShell profile (creating it if it doesn't exist) and appends the `genesis` tool to it.
```powershell
$GenesisFunc = @'
function genesis {
    $path = ".ai\prompts"
    if (!(Test-Path -Path $path)) {
        New-Item -ItemType Directory -Force -Path $path | Out-Null
    }
    Write-Host "⬇️  Initializing Genesis System..." -ForegroundColor Cyan
    
    $base = "https://raw.githubusercontent.com/en4ble1337/The-Genesis-System-Project-Initialization-Workflow/main"
    
    Invoke-WebRequest -Uri "$base/phase1.md" -OutFile "$path\01_prd.md"
    Invoke-WebRequest -Uri "$base/phase2.md" -OutFile "$path\02_arch.md"
    Invoke-WebRequest -Uri "$base/phase3.md" -OutFile "$path\03_scaffold.md"
    
    Write-Host "✅ Genesis Protocols Loaded in $path" -ForegroundColor Green
}
'@

if (!(Test-Path $PROFILE)) {
    New-Item -Type File -Path $PROFILE -Force | Out-Null
}

Add-Content -Path $PROFILE -Value $GenesisFunc
Write-Host "Installation Complete. Reloading profile..." -ForegroundColor Green
. $PROFILE
```

### Step 2: Use It

Go to any project folder in PowerShell and type:
```powershell
genesis
```

### Step 3: Verify It Worked

Run this command to confirm the files downloaded correctly:
```powershell
ls .ai\prompts
```

You should see a list of the 3 markdown files (`01_prd.md`, `02_arch.md`, `03_scaffold.md`) confirming the download was successful.

### Alternative: Git Bash

If you prefer using Git Bash instead of PowerShell, use the same command provided for Mac/Linux. Simply paste it into your Git Bash window and it works identically.

---

## Using the Genesis Files

Now that you have the files in `.ai/prompts/`, you can access them in your AI editor.

Most modern AI code editors (Cursor, Windsurf, Project IDX, VS Code Copilot) use the `@` symbol to reference files.

### Syntax

Open your AI Chat panel and type the `@` symbol followed by the filename:
```
@01_prd.md
@02_arch.md
@03_scaffold.md
```

**Tip:** You usually only need to type `@01` or `@prd` and the editor will show a dropdown menu for you to select the file.
