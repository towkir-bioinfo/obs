
# Bluetooth Failure on Windows — Full Troubleshooting Log

**System:** KERNELOS-PC (Windows 10/11, Realtek Bluetooth 5 Adapter)
**Symptom:** Bluetooth could not discover or connect to any device. Later, the HB19 headset paired but produced no audio.

---

## Root Cause Summary

Three Bluetooth driver services had been set to **Disabled (Start = 4)** in the registry:

| Service | Purpose | Bad Value | Fixed Value |
|---|---|---|---|
| `BthEnum` | Main Bluetooth enumerator | 4 (Disabled) | 3 (Manual) |
| `RFCOMM` | Serial-over-Bluetooth protocol | 4 (Disabled) | 3 (Manual) |
| `BthLEEnum` | Bluetooth Low Energy enumerator | 4 (Disabled) | 3 (Manual) |

A **disabled service** causes Windows to report **Code 32 (`CM_PROB_DISABLED_SERVICE`)** on every dependent device — which blocks the entire Bluetooth stack from initializing, even when the adapter's own driver is healthy.

This is a common side effect of "debloat" scripts, gaming optimizers, and privacy tools that disable services they consider non-essential.

---

## Diagnostic Commands

### 1. Check hardware and service status
```powershell
Get-PnpDevice -Class Bluetooth | Format-Table FriendlyName, Status, InstanceId -AutoSize
Get-Service -Name bthserv, BTAGService | Format-Table Name, Status, StartType -AutoSize
```

### 2. Find devices in error state
```powershell
Get-PnpDevice -PresentOnly -Status ERROR,DEGRADED,UNKNOWN -ErrorAction SilentlyContinue |
    Where-Object {$_.Class -eq "Bluetooth"} |
    Format-Table FriendlyName, Status, Problem, InstanceId -AutoSize
```

### 3. Pull detailed problem codes
```powershell
Get-PnpDevice -Class Bluetooth | Get-PnpDeviceProperty | Where-Object {
    $_.KeyName -eq "DEVPKEY_Device_HasProblem" -or
    $_.KeyName -eq "DEVPKEY_Device_ProblemCode" -or
    $_.KeyName -eq "DEVPKEY_Device_DriverVersion" -or
    $_.KeyName -eq "DEVPKEY_Device_InstallState"
} | Select-Object InstanceId, KeyName, Data | Format-Table -AutoSize
```

### 4. Check driver service Start values (the key diagnostic)
```powershell
$services = @("BTHPORT", "BTHUSB", "BthEnum", "RFCOMM", "BthLEEnum", "bthserv", "BTAGService")
$results = foreach ($svc in $services) {
    $path = "HKLM:\SYSTEM\CurrentControlSet\Services\$svc"
    if (Test-Path $path) {
        $start = (Get-ItemProperty -Path $path -Name "Start" -ErrorAction SilentlyContinue).Start
        $desc = switch ($start) {
            0 { "Boot" }
            1 { "System" }
            2 { "Automatic" }
            3 { "Manual" }
            4 { "DISABLED  <-- PROBLEM" }
            default { "Not set" }
        }
        [PSCustomObject]@{ Service = $svc; Start = $start; Meaning = $desc }
    }
}
$results | Format-Table -AutoSize
```

**Start value meanings:**
- `0` = Boot
- `1` = System
- `2` = Automatic
- `3` = Manual ✅ (correct for driver services)
- `4` = Disabled ❌ (this is the problem)

---

## The Fix

### Step 1 — Re-enable the core Bluetooth services
```powershell
Set-Service -Name "bthserv" -StartupType Automatic
Set-Service -Name "BTAGService" -StartupType Automatic
Start-Service -Name "bthserv"
Start-Service -Name "BTAGService"
```

### Step 2 — Fix the disabled driver services in the registry
```powershell
$services = @("BthEnum", "RFCOMM", "BthLEEnum")
foreach ($svc in $services) {
    $path = "HKLM:\SYSTEM\CurrentControlSet\Services\$svc"
    Set-ItemProperty -Path $path -Name "Start" -Value 3 -Type DWord
    Write-Host "Fixed: $svc -> Start = 3 (Manual)" -ForegroundColor Green
}
```

### Step 3 — Verify the change
```powershell
$services = @("BthEnum", "RFCOMM", "BthLEEnum")
$results = foreach ($svc in $services) {
    $path = "HKLM:\SYSTEM\CurrentControlSet\Services\$svc"
    $start = (Get-ItemProperty -Path $path -Name "Start").Start
    [PSCustomObject]@{ Service = $svc; Start = $start }
}
$results | Format-Table -AutoSize
```
Expected output: **all three = 3**

### Step 4 — Full shutdown (NOT restart)
The driver services only load at boot time and a restart does not fully reset the PnP tree.

1. Close PowerShell
2. Start → Power → **Shut down**
3. Wait 30 seconds
4. Power back on

### Step 5 — Verify Bluetooth is healthy
```powershell
Get-PnpDevice -Class Bluetooth | Format-Table FriendlyName, Status -AutoSize
Get-Service bthserv, BTAGService | Format-Table Name, Status, StartType -AutoSize
```

**Expected result — all `OK`:**

| Device | Status |
|---|---|
| Realtek Bluetooth 5 Adapter | OK |
| Microsoft Bluetooth Enumerator | OK |
| Microsoft Bluetooth LE Enumerator | OK |
| Bluetooth Device (RFCOMM Protocol TDI) | OK |
| bthserv | Running / Automatic |
| BTAGService | Running / Automatic |

---

## Secondary Issue — HB19 Headset Connected but No Audio

### Symptom
- HB19 showed **"Connected"** in Bluetooth settings
- Sound Output dropdown only showed **"Speaker (Realtek High Definition Audio)"**
- Device Manager Hardware tab listed HB19 as **"Bluetooth Peripheral Device"** (not a headset)
- No Stereo (A2DP) audio endpoint was ever created

### Cause
The initial pairing completed at the **Bluetooth link layer** but never negotiated the **Stereo (A2DP) audio profile**. Windows cached that incomplete pairing and does not retry the profile negotiation on its own.

Common trigger: **another Bluetooth host (phone, tablet) grabs the headset** the moment it enters pairing mode, so the laptop only gets the low-quality Hands-Free profile — or none at all.

### Fix — Clean Re-Pair
1. Settings → Bluetooth & devices → **HB19** → **⋯** → **Remove device**
2. **Turn Bluetooth OFF on your phone** and every other device that has ever paired with the HB19
3. Reset HB19: power **off** → hold **both "+" and "–"** for **4 seconds** → LED must flash **red and blue alternately**
4. Settings → **Add device → Bluetooth → HB19**
5. The moment it says "Connected," left-click the **speaker icon** on the taskbar and select **HB19 Stereo**

### If HB19 Stereo still doesn't appear
Reinstall the audio and Bluetooth drivers:

1. Device Manager → **Sound, video and game controllers** → right-click **Realtek High Definition Audio** → **Uninstall device** → check "Delete driver"
2. Device Manager → **Bluetooth** → right-click **Realtek Bluetooth 5 Adapter** → **Uninstall device** → check "Delete driver"
3. **Fully shut down** → power on
4. Re-pair HB19 using the 5-step process above

---

## What Not to Blame

**The "Activate Windows" yellow banner is NOT the cause.**
- Activation only locks *personalization* (wallpaper, themes, colors, lock screen)
- It does **not** block audio output selection, Bluetooth pairing, or device management
- Proof: a wired headphone could be selected in the Output dropdown while the yellow banner was still showing
- If audio ever sounds like a phone call, Windows fell back to the Hands-Free profile — just re-select **HB19 Stereo**

---

## Prevention

- ❌ **Do not run** "debloat" scripts, one-click optimizers, or privacy tools that disable Windows services — they are what set `BthEnum`, `RFCOMM`, and `BthLEEnum` to Disabled
- ✅ If Bluetooth ever "disappears" after a Windows update, check the Start values of these three services first:
  - `HKLM\SYSTEM\CurrentControlSet\Services\BthEnum`   → Start = 3
  - `HKLM\SYSTEM\CurrentControlSet\Services\RFCOMM`    → Start = 3
  - `HKLM\SYSTEM\CurrentControlSet\Services\BthLEEnum` → Start = 3
- ✅ When re-pairing any Bluetooth headset, **turn off Bluetooth on your phone first** so the laptop gets the Stereo (A2DP) profile
- ✅ Prefer the **manufacturer's Bluetooth driver** over Windows Update generic drivers for Realtek adapters

---

## Quick Reference — Common Bluetooth Problem Codes

| Code | Name | Meaning |
|---|---|---|
| 10 | `CM_PROB_FAILED_START` | Device failed to start (often power-management) |
| 22 | `CM_PROB_DISABLED` | Device disabled by user |
| 28 | `CM_PROB_FAILED_INSTALL` | Driver not installed |
| 31 | `CM_PROB_FAILED_ADD` | Driver failed to load |
| 32 | `CM_PROB_DISABLED_SERVICE` | Driver service set to Disabled in registry |
| 43 | `CM_PROB_FAILED_POST_START` | Driver reported failure to Windows |
| 45 | `CM_PROB_PHANTOM` | Device no longer present (ghost entry) |

---

## Commands Used to Remove Phantom / Ghost Devices

`Remove-PnpDevice` is **not** a native cmdlet. Use `pnputil` instead:

```powershell
pnputil /remove-device "USB\VID_0A12&PID_0001\5&22B8DD10&0&2"
pnputil /scan-devices
```

Or, for hidden/ghost entries, use **Device Manager → View → Show hidden devices** and uninstall from there.
