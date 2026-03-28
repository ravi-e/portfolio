# API Reference: Inventory Manager

!!! info "About this Sample"
     **Context:** This sample demonstrates documentation for a RESTful resource.  
    **Key Skills:** Structured parameter tables, JSON syntax highlighting, and standard HTTP error mapping.

The Inventory Manager API allows developers to programmatically manage warehouse stock, track shipments, and update product availability.

## Authentication

All API requests require a Bearer Token passed in the HTTP header:
`Authorization: Bearer <YOUR_API_KEY>`

---

## Get Product Details
`GET /v1/products/{product_id}`

Retrieves comprehensive metadata for a specific inventory item, including real-time stock levels across all warehouse locations.

### Path Parameters
| Parameter | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `product_id` | `string` | **Yes** | The unique UUID of the product. |

### Query Parameters
| Parameter | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `include_location` | `boolean` | `false` | If true, returns a breakdown of stock by warehouse ID. |

### Response Examples

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
      "error": "product_not_found",
      "message": "The requested product ID does not exist in the catalog."
    }
  ```

---

## Update Stock Level
`PATCH /v1/products/{product_id}/stock`

Updates the quantity of a product. 

### Request Body
| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `adjustment` | `integer` | **Yes** | The amount to add or subtract from stock. |
| `reason` | `string` | No | A note for the audit log (e.g., "Restock", "Damaged"). |

### Request Example
```json
{
  "adjustment": 50,
  "reason": "New shipment received"
}
```

### Response Example

```json
{
  "id": "prod_99x21",  
  "new_total": 1500,  
  "updated_at": "2026-03-28T10:15:00Z"  
}
```

## Standard Error Codes

| Status Code | Error String (Code) | Description |
| :--- | :--- | :--- |
| `400` | `invalid_adjustment` | The adjustment value must be a non-zero integer. |
| `401` | `unauthorized` | Authentication failed. Missing or invalid API key in the header. |
| `403` | `forbidden` | The API key does not have permission to modify this specific warehouse. |
| `404` | `product_not_found` | The requested `product_id` does not exist in the database. |
| `429` | `rate_limit_exceeded` | Account quota reached. Please throttle requests to 10 per second. |
| `500` | `internal_server_error` | An unexpected error occurred on our end. Please try again later. |