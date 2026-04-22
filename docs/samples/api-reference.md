# API Reference: Smart Vehicle Platform

!!! info "About this Sample"
     **Context:** This sample demonstrates documentation for a RESTful resource.  
    **Key Skills:** Structured parameter tables, JSON syntax highlighting, and standard HTTP error mapping.

## Overview

The Smart Vehicle Platform API enables applications to interact with connected electric vehicles such as the Ather Rizta, along with supporting systems like inventory and service management.

This API provides access to:

- Real-time vehicle telemetry (battery, ride data)
- Product and component inventory (e.g., motor units, spare parts)
- Service and diagnostics workflows

## How this API powers the product

The features described in the [Getting Started](getting-started.md) guide are powered by this API.

For example:  

- Battery status → `GET /vehicles/{id}/battery`
- Ride history → `GET /vehicles/{id}/rides`
- Vehicle diagnostics → `GET /vehicles/{id}/health`
- Spare part tracking → `GET /v1/products/{product_id}`

## Architecture Overview

```text
Mobile App → API Layer → Vehicle Cloud → Scooter
                         ↓
                  Inventory System
```

This architecture illustrates how:

- User actions in the app trigger API calls 
- The API interacts with both vehicle systems and backend services
- Inventory and telemetry systems work together to support operations     

Base URL:

`https://api.smartvehicle.com/v1`

## Authentication

All requests require authentication using a Bearer token.

### Example
Authorization: Bearer <access_token>

### Token lifecycle
- Tokens expire after 60 minutes
- Refresh tokens must be used for renewal

### Error responses  
- 401 Unauthorized – Invalid or expired token

## Rate Limits

To ensure platform stability, API usage is rate-limited:

- **100 requests per minute per API key**
- Exceeding this limit returns: `429 Too Many Requests`

---

## Getting Started

### 1. Obtain API credentials  
Sign up on the developer portal to receive your API key and access token.

### 2. Make your first request

    curl -X GET https://api.smartvehicle.com/vehicles \
      -H "Authorization: Bearer <token>"

### 3. Sample response

    {
    "vehicles": [...]
    }


## Use cases

- **Track spare part inventory:** Retrieve real-time stock levels for critical components such as traction motors and battery modules.
- **Enable service workflows:** Update inventory levels when parts are consumed during maintenance
- **Power diagnostics dashboards:** Combine vehicle telemetry and inventory data to predict service needs.

---

## API Reference

## Products API

The Products API allows applications to retrieve and manage inventory data for vehicle components and spare parts.

### Get Product Details
`GET /v1/products/{product_id}`

Retrieves metadata for a specific inventory item, including real-time stock levels across warehouse locations.

#### Path Parameters
| Parameter | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `product_id` | `string` | **Yes** | The unique identifier of the product. |

#### Query Parameters
| Parameter | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `include_location` | `boolean` | `false` | If true, returns a breakdown of stock by warehouse ID. |

#### Response Examples

=== "200 OK"
  ```json
    {
      "id": "rizta_pwr_unit",
      "sku": "ATHR-GEN3-MUM",
      "name": "PMSM Traction Motor Cog",
      "total_stock": 350,
      "status": "warp_mode_active",
     "last_updated": "2026-03-28T10:00:00Z"
    }
  ```

=== "404 Not Found"
  ```json
    {
      "error_code": "product_not_found",
      "message": "The requested product ID does not exist in the catalog.",
      "resolution": "Verify the product ID or query the products list endpoint."
    }
  ```

---

### Update Stock Level
`PATCH /v1/products/{product_id}/stock`

Updates the quantity of a product. 

#### Request Body
| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `adjustment` | `integer` | **Yes** | The quantity to add or subtract from stock. |
| `reason` | `string` | No | A note for the audit log (e.g., "Restock", "Damaged"). |

#### Request Example
```json
{
  "adjustment": 50,
  "reason": "New shipment received"
}
```

#### Response Example

```json
{
  "id": "prod_99x21",  
  "new_total": 1500,  
  "updated_at": "2026-03-28T10:15:00Z"  
}
```

## Standard Error Codes

All errors follow a consistent structure:
```JSON
{
  "error_code": "string",
  "message": "Human-readable description",
  "resolution": "Suggested corrective action"
}
```

| Status Code | Error String (Code) | Description |
| :--- | :--- | :--- |
| `400` | `invalid_adjustment` | The adjustment value must be a non-zero integer. |
| `401` | `unauthorized` | Authentication failed. Missing or invalid API key in the header. |
| `403` | `forbidden` | The API key does not have permission to modify this specific warehouse. |
| `404` | `product_not_found` | The requested `product_id` does not exist in the database. |
| `429` | `rate_limit_exceeded` | Account quota reached. Please throttle requests to 10 per second. |
| `500` | `internal_server_error` | An unexpected error occurred on our end. Please try again later. |       

---

!!! note "About this sample"
    This documentation is a fictional example created as part of a technical writing portfolio.  
    It is not affiliated with or endorsed by Ather Energy.

    References to the Ather Rizta and related systems are used purely for illustrative purposes to demonstrate documentation concepts and do not reflect actual product behavior.