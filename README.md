# SystemAnalyserOnSteroids
Creating a system diagnose that is meant to be uploadet to AI, to fix Problems or Optimize your PC.
 
You can youse or edit the provided prompt txt file, to let AI do a generic low risk gaming optimization for your pc.


Windows 11 Gaming Full Diagnostics
Read-only Windows 11 diagnostics script focused on gaming-relevant areas: hardware, display/EDID, GPU/DirectX, registry settings, scheduled tasks, drivers, services, power configuration, network settings, event logs, crash/WER data, startup entries, and basic junk analysis.
Important note
Administrator rights are required for a complete diagnostic run. The PowerShell script checks this automatically and relaunches itself through UAC when needed. Without administrator rights, important areas may be unavailable, including HKLM registry branches, drivers, event logs, system-wide scheduled tasks, and some hardware information.
The script does not modify the system. It only reads diagnostic data and writes report files to the selected output folder.
Quick start
Download and extract the repository or ZIP archive.
Start `Start-Diagnostics.cmd` by double-clicking it.
Accept the UAC prompt.
The report is written by default to:
the current user's Desktop Known Folder,
subfolder `GamingFullDiagnostics`,
file `gaming_full_diagnostics_YYYYMMDD_HHMMSS.txt`.
The output folder is resolved through Windows Known Folders. This supports OneDrive Desktop redirection, redirected user profiles, and non-English Windows language packs.
PowerShell usage
```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\gaming_full_diagnostics.ps1
```
Options:
```powershell
# Use a custom output folder
.\gaming_full_diagnostics.ps1 -OutDir "D:\Diag"

# Set the exact report file path
.\gaming_full_diagnostics.ps1 -OutFile "D:\Diag\my_report.txt"

# Change the event log time window, default: 45 days
.\gaming_full_diagnostics.ps1 -EventDays 14

# Skip DxDiag
.\gaming_full_diagnostics.ps1 -SkipDxDiag

# Do not attempt automatic UAC elevation
.\gaming_full_diagnostics.ps1 -NoElevate

# Do not wait for Enter before closing the console
.\gaming_full_diagnostics.ps1 -NoPause
```
Compatibility
Target system:
Windows 11
Windows PowerShell 5.1
Administrator rights for a full scan
Language packs:
No hardcoded user profile paths are used.
The script prefers CIM, registry data, enum/raw values, and Windows Known Folders over localized console text.
Raw output from Windows tools such as `powercfg`, `netsh`, `driverquery`, `pnputil`, `systeminfo`, and `dxdiag` may still appear in the installed Windows display language. This is expected because those tools localize their own output.
Privacy warning
The report can contain sensitive data, including:
username and host name,
hardware identifiers,
installed software and drivers,
startup entries and scheduled tasks,
event log messages and crash/WER references,
user profile paths,
network adapter information.
Review and redact the report before sharing it in GitHub issues, Discord, forums, or public support tickets.
Changes from the original PC-specific version
Removed the hardcoded path `C:\Users\222\Desktop\REG_DIAGNOSE`.
Removed personal branding and single-PC assumptions.
Removed the embedded Base64 copy from the BAT launcher to make the repository maintainable.
Added UAC self-elevation in the PowerShell script.
Added dynamic Known-Folder-based output path resolution.
Added timestamped report filenames to avoid accidental overwrites.
Added parameters for output path, event log range, DxDiag skipping, elevation control, and no-pause mode.
Improved compatibility with localized Windows installations by preferring CIM/registry/raw values over localized display strings where practical.
Converted script output, comments, README, changelog, and launcher to English.
Added `.gitignore` for generated reports and diagnostic artifacts.

v5.2-lightweight notes
Runtime-irrelevant PowerShell comments were removed from the main script.
The script keeps English output while continuing to avoid language-pack-sensitive parsing where practical.
Progress counting was corrected so sub-steps no longer inflate the main progress total.
Event log message handling is more null-safe.
Folder-size measurement now streams through `Measure-Object` instead of storing all files in memory first.
