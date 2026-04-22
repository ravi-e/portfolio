# CLI Reference: Rizta DevKit

!!! info "About this Sample"
    **Goal:** Provide a command-level reference for interacting with the Rizta DevKit CLI.  
    **Key Skills:** CLI documentation structure, command syntax design, parameter clarity, and mapping CLI actions to API behavior.

The Rizta CLI allows developers to interact with the Smart Vehicle Platform directly from the command line.

---

## How the CLI maps to the API

Each CLI command corresponds to one or more API endpoints.

  | CLI Command | API Endpoint |
  |----------	|----------	|
  | `rizta auth --pair` |  `POST /auth/pair` |
  | `rizta status` | `GET /vehicles/{id}/status` |
  | `rizta rides` |`GET /vehicles/{id}/rides` |

For detailed request and response structures, see the [API Reference](api-reference.md).

---

## Command structure

All commands follow this pattern:

``` bash
rizta <command> [options]
```

-   `<command>` specifies the action
-   `[options]` modify behavior or provide required inputs

---

## Global options

| Option | Description |
|----------------|---------------------------------|
| `--help` | Displays help for a command |
| `--version` | Shows CLI version  |
| `--output json` | Formats output as JSON |

---

## Authentication Commands

### Pair a vehicle

``` bash
rizta auth --pair
```

Pairs your local CLI with a scooter using VIN-based authentication.

#### Options

| Option | Required | Description |
|--------------|----------|------------------------------------------|
| `--vin` | Yes | Vehicle Identification Number |
| `--profile` | No | Riding profile (`eco`, `zip`, `warp`) |

#### Example

``` bash
rizta auth --pair --vin "RIZTA123456" --profile warp
```

#### Output

``` json
{
  "status": "paired",
  "vehicle_id": "rizta_001",
  "profile": "warp"
}
```

---

## Vehicle Commands

### Get vehicle status

``` bash
rizta status --vehicle-id <id>
```

Retrieves real-time vehicle telemetry including battery, range, and
operational state.

#### Example

``` bash
rizta status --vehicle-id "rizta_001"
```

#### Output

``` json
{
  "soc": 88,
  "range_km": 112,
  "status": "ready"
}
```

---

### Get ride history

``` bash
rizta rides --vehicle-id <id>
```

Returns recent ride sessions and statistics.

#### Example

``` bash
rizta rides --vehicle-id "rizta_001"
```

#### Output

``` json
{
  "rides": [
    {
      "date": "2026-03-27",
      "distance_km": 24,
      "mode": "zip"
    }
  ]
}
```

---

## Diagnostics Commands

### Check vehicle health

``` bash
rizta health --vehicle-id <id>
```

Provides diagnostic information about the vehicle system.

#### Output

``` json
{
  "motor_status": "optimal",
  "battery_health": "good",
  "alerts": []
}
```

---

## Error Handling

CLI errors follow a structured format:

``` json
{
  "error_code": "string",
  "message": "Human-readable description",
  "resolution": "Suggested corrective action"
}
```

---

## Common CLI Errors

| Error | Cause | Resolution |
|-------|-------|------------|
| `authentication_failed` | Invalid pairing session | Re-run `rizta auth --pair` |
| `vehicle_not_found` | Incorrect vehicle ID | Verify VIN and pairing |
| `rate_limited` | Too many requests | Reduce command frequency |

---

!!! note "About this sample"
    This documentation is a fictional example created as part of a technical writing portfolio.  
    It is not affiliated with or endorsed by Ather Energy.

    References to the Ather Rizta and related systems are used purely for illustrative purposes to demonstrate documentation concepts and do not reflect actual product behavior.
