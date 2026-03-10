---
name: openclaw-uninstaller
description: Completely and thoroughly uninstall OpenClaw (AI assistant) from the current system, leaving no residual files, configs, processes, or environment variables. Use this skill whenever the user asks to uninstall, remove, clean up, or wipe OpenClaw or any AI assistant installed on the device. Triggers on phrases like "卸载 openclaw", "uninstall openclaw", "remove openclaw", "clean up AI", "彻底卸载", or any request to generate an uninstall script for OpenClaw.
---

# OpenClaw Uninstaller Skill

Completely and thoroughly uninstall OpenClaw from the current system, leaving zero residual files, configs, processes, or environment variables.

---

## Workflow

### Step 1: System Environment Collection

Before generating any script, fully investigate the current system environment. Information to collect includes:

- Operating system type, distribution, and version
- Current user identity and home directory path
- Shell type in use and the locations of all its config files
- Every file and directory on the system related to openclaw (full disk search)
- All openclaw-related processes currently running
- Which package managers are installed (apt, yum, brew, snap, flatpak, npm, pip, etc.) and whether openclaw appears in any of them
- The location of any openclaw binaries
- Whether any system services reference openclaw (systemd, launchd, init.d, etc.)
- Whether any shell config files contain openclaw-related environment variables, PATH entries, or aliases
- Whether any cron jobs reference openclaw
- Whether any temporary directories contain openclaw-related files

Once collection is complete, analyze the findings and proceed to Step 2.

---

### Step 2: Generate uninstall_ai.sh

Using only what was actually discovered in Step 1, write a script named `uninstall_ai.sh`. The script must be organized into clear steps, each printing a description of what it is doing so the user can follow along. The script must be resilient — if a path does not exist or an operation fails, the script should continue rather than abort.

The script must cover all of the following areas, with specific paths and methods determined entirely by real findings from Step 1:

**Process cleanup**: Terminate all running openclaw-related processes.

**Service cleanup**: Stop and disable all openclaw-related system services, and remove their associated service definition files.

**Binary cleanup**: Remove all openclaw executable files.

**Config directory cleanup**: Remove all openclaw-related configuration folders and files from both user and system directories.

**Data and log cleanup**: Remove openclaw's data directories, log directories, and cache directories.

**Package manager uninstall**: Formally uninstall openclaw through whichever package managers were detected.

**Environment variable cleanup**: Remove all openclaw-related environment variables, PATH entries, and aliases from every shell config file found.

**Cron job cleanup**: Remove all openclaw-related entries from the user's crontab.

**Temp file cleanup**: Clear all openclaw-related files from temporary directories.

**Final verification**: After all steps complete, search the entire system for any remaining openclaw-related files or processes and report the findings to the user. If the system is clean, confirm success. If anything remains, list the specific paths.

Save the finished script to the current working directory and make it executable.

---

### Step 3: Execute the Script

Run the generated script, capture its full output, and display it so the user can see the result of every step and confirm whether OpenClaw has been completely removed.

---

## Notes

- Step 1 is mandatory. Never skip it and generate a generic script based on assumptions.
- All script content must be based on real discoveries, not guesses or boilerplate.
- If the current user lacks sufficient permissions for certain operations, inform the user that sudo may be required.
- Every removal operation in the script must be written so that it does not cause the script to exit if the target does not exist.