# Getting Started: Rizta DevKit (v3.0)

!!! info "About this Sample"  
    **Goal:** Onboard developers to the Ather Rizta IoT ecosystem.  
    **Key Skills:** Hardware-software prerequisites, CLI installation, and "Warp Mode" authentication logic.

Welcome to the **Rizta DevKit**. This guide will help you connect your local environment to your scooter’s onboard computer (Dashboard) to start pulling telemetry data.

---

## Prerequisites

Before you begin, ensure you have the following:

* **Hardware:** An Ather Rizta (Gen 3) with an active **Ather Connect Pro** subscription.
* **Software:** Node.js v18.0 or higher.

---

## 1. Install the CLI

The Rizta Command Line Interface (CLI) is the primary tool for communicating with the scooter's API. Install it globally using `npm`:

```bash
npm install -g @ather/rizta-cli
```

## 2. Authenticate your scooter

To ensure your data doesn't end up on someone else's dashboard, you must pair your scooter using your unique VIN (Vehicle Identification Number).

1. Run the following command in your terminal:
   ```Bash
   rizta auth --pair
   ```
2. When prompted for your "Riding Profile," select your preferred mode:
    * `Eco`: Max range, minimum API polling.
    * `Zip`: Balanced performance.
    * `Warp`: High-frequency data streaming. Warning: May cause spontaneous smiles during Mumbai traffic.

## 3. Make the first API call
Let's verify the connection by checking your current battery percentage and estimated range.

**Example Request**
```Bash
rizta status --id "rizta_pwr_unit"
```
**Example Response**
```json
{
  "vehicle": "Rizta_Z_Limited",
  "location": "Mumbai_West",
  "soc": 88,
  "range_km": 112,
  "status": "ready_to_zip",
  "easter_egg": "bike_of_scooters"
}
```
---

## Next steps
Now that you're connected, explore the following resources:

* [Troubleshooting](troubleshooting.md): What to do if your Halo Dashboard goes dark.

