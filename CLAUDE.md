# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A knowledge base for Active Directory / Entra ID threat hunting, not a software project. It has no build system, no dependencies, no tests and no CI. Content is Markdown write-ups, PowerShell snippet collections, config files and sample BloodHound data. Everything is in English.

## Layout and conventions

- `PowerShell/*.ps1` are **scratchpad-style snippet collections, not runnable scripts**. They mix bare URLs (MITRE ATT&CK, Microsoft Learn) and `#` comments with commands meant to be run one at a time in an interactive session against a lab DC (e.g. `Enter-PSSession -ComputerName DC01`, then `Get-WinEvent` / `Get-ADUser` queries). Running a whole file will fail on the bare URL lines. Keep this style when adding snippets: a `#` heading, the reference URL, then the commands. Requires the `ActiveDirectory` RSAT module and domain access.
- `Different_hunting_methods/`, `Azure_Active_Directory/`, `Security_compliance_toolkit_and_baselines/`, `Advanced_monitoring/` hold long-form write-ups. They share one structure: a `# <Title>!` heading, then "We start with a list of MITRE techniques" (tactic/technique links), then "The Windows Event ID's for the MITRE techniques" (Event ID + Microsoft Learn link), then the hands-on part (ADRecon, AzureADRecon, Microsoft Sentinel / Defender for Endpoint advanced hunting KQL, Policy Analyzer, Security Onion), ending with a `*HAPPY ...!*` line. Screenshots live in each folder's `Images/` subfolder and are referenced by relative path.
- `MITRE_ATT&CK_Techniques_Windows_Eventlog_IDs.md` is the central mapping of ATT&CK technique → Windows Security Event ID (`**4769(S, F): ...**` bold line followed by the Microsoft Learn URL). `Links.txt` is a flat list of reference links in the same spirit.
- `Advanced_monitoring/Security_Onion_2.3/` contains real config: `sysmon-config.xml` and `winlogbeat.yml` for shipping Windows events to Security Onion. `Commands.sh` holds the related Windows commands (despite the `.sh` extension): `winlogbeat.cmd test config ...` and `Sysmon64.exe -i sysmon-config.xml`.
- `*_BloodHound.zip` at the root are SharpHound collection output (JSON: computers, users, groups, containers, domains, gpos, ous) from a lab domain, to be imported into BloodHound. `BloodHound_and_SharpHound.txt` documents the Kali setup (`apt install bloodhound`, `neo4j console`) and SharpHound collection methods. `WSL_Kali_Post_Installation.txt` and `WSLg_and_Kali_Win-Kex.txt` cover the Kali-on-WSL attacker workstation.

## Editing notes

- Content is offensive/defensive security material for an authorized lab. Keep new material tied to a MITRE technique and the matching Event ID, consistent with existing files.
- `.DS_Store` files are committed despite `.gitignore`; don't add more.
- Don't modify the BloodHound zips; add new collections as new timestamped zips.
