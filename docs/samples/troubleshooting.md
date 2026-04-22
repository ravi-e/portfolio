# Troubleshooting: Rizta DevKit

!!! info "About this Sample"
    **Goal:** Help developers quickly diagnose and resolve common issues when using the Rizta DevKit and CLI.  
    **Key Skills:** Error-driven documentation, actionable resolutions, and mapping failures to system components.

This guide helps you identify and resolve common issues when connecting to and interacting with your Rizta scooter.

---

## How to use this guide

1.  Identify the error message or symptom
2.  Locate the issue in the table below
3.  Follow the recommended resolution steps

If the issue persists, verify your setup using the [Getting Started guide](getting-started.md).

---

## Common issues

| Issue | Possible Cause | Resolution |
|------|---------------|------------|
| CLI command not found | CLI not installed or not in PATH | Reinstall using `npm install -g @ather/rizta-cli` and restart your terminal |
| Authentication fails (`authentication_failed`) | Expired or invalid session | Re-run `rizta auth --pair` |
| Vehicle not found (`vehicle_not_found`) | Incorrect vehicle ID or VIN not paired | Verify VIN and ensure successful pairing |
| No data returned from `rizta status` | Vehicle offline or not connected | Ensure scooter is powered on and has network connectivity |
| Rate limit exceeded (`rate_limited`) | Too many requests in short time | Reduce request frequency or add delays between commands |

---

## Connectivity issues

### Scooter not responding

**Symptoms**  
CLI commands may return no data, or requests may time out.

**Possible causes**  
The scooter may be powered off, there may be network connectivity issues, or there could be a delay in backend services.

**Resolution**  
Ensure that the scooter is powered on, check mobile network availability, and retry the request after a few minutes.

---

## Authentication issues

### Pairing fails

**Symptoms**  
You may encounter an `authentication_failed` error, or the pairing command may not complete successfully. 

**Possible causes**  
This issue may occur due to an incorrect VIN or an expired session token.

**Resolution**   
Verify that the VIN is accurate and restart the pairing process using the following command:

``` bash
rizta auth --pair
```

---

## Data inconsistencies

### Battery or range values seem incorrect

**Possible causes**  
This issue may be caused by a delay in telemetry updates or the use of cached data.

**Resolution**  
Retry the command after a short interval, and ensure that you are using Warp mode to enable real-time data updates.

---

## When to escalate

If issues persist:

-  Re-run the setup from the [Getting Started](getting-started.md) guide
-  Verify CLI version using:

``` bash
rizta --version
```

---

## Related resources

- [Getting Started](getting-started.md)
- [CLI Reference](cli-reference.md)
- [API Reference](api-reference.md)

---

!!! note "About this sample"
    This documentation is a fictional example created as part of a technical writing portfolio.  
    It is not affiliated with or endorsed by Ather Energy.

    References to the Ather Rizta and related systems are used purely for illustrative purposes to demonstrate documentation concepts and do not reflect actual product behavior.