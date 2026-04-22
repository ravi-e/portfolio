# Getting Started: Rizta DevKit (Connected EV Platform)

!!! info "About this Sample"  
    **Goal:** Onboard developers to the Ather Rizta connected vehicle ecosystem.  
    **Key Skills:** Hardware-software prerequisites, CLI installation, and API-driven telemetry access.

Welcome to the **Rizta DevKit**. This guide will help you connect your local environment to your scooter’s onboard computer (Dashboard) to start pulling telemetry data.

The DevKit CLI acts as a bridge between your local machine and the **Smart Vehicle Platform API**.

## How it works

```text
CLI → API Layer → Vehicle Cloud → Scooter
```

- The CLI sends requests to the Smart Vehicle Platform API
- The API retrieves data from the vehicle cloud
- The scooter streams telemetry back to your application

For detailed endpoint behavior, see the [API Reference](api-reference.md).

---

## Prerequisites

Before you begin, ensure you have the following:

* **Hardware:** An Ather Rizta (Gen 3) with an active **Ather Connect Pro** subscription.
* **Software:** Node.js v18.0 or higher.

---

## 1. Install the CLI

The Rizta Command Line Interface (CLI) is the primary tool for interacting with the platform. 

Install it globally using `npm`:

```bash
npm install -g @ather/rizta-cli
```

## 2. Authenticate your scooter

To securely access your vehicle data, you must pair your scooter using its VIN (Vehicle Identification Number).

1. Run the following command in your terminal:
   ```Bash
   rizta auth --pair
   ```
2. When prompted for your "Riding Profile," select your preferred mode:
    * `Eco`: Max range, minimum API polling.
    * `Zip`: Balanced performance.
    * `Warp`: High-frequency data streaming. 

## 3. Make your first API call
Verify your setup by retrieving battery and range information.

**Example Request**
```Bash
rizta status --vehicle-id "rizta_001"
```
**Example Response**
```json
{
  "vehicle": "Rizta_Z_Limited",
  "location": "Mumbai_West",
  "soc": 88,
  "range_km": 112,
  "status": "ready",
  "easter_egg": "bike_of_scooters"
}
```

## Common errors

| Error | Cause | Resolution |
|----------	|----------	|----------	|
| `authentication_failed` | Invalid or expired session | Re-run `rizta auth --pair` |
| `vehicle_not_found` | Incorrect vehicle ID | Verify VIN and pairing |
| `rate_limited` | Too many requests | Reduce polling frequency	|

---

## Next steps
Now that you're connected, explore the following resources:

* [API Reference](api-reference.md): Understand available endpoints and data models
* [Troubleshooting](troubleshooting.md): Resolve common connectivity and telemetry issues

---

!!! note "About this sample"
    This documentation is a fictional example created as part of a technical writing portfolio.  
    It is not affiliated with or endorsed by Ather Energy.

    References to the Ather Rizta and related systems are used purely for illustrative purposes to demonstrate documentation concepts and do not reflect actual product behavior.