# Smart Paathshala Payment API Documentation

<p align="center">
  <img src="./assets/images/smart-pathshala-banner.png" alt="Smart Paathshala Banner" width="100%">
</p>

## Overview

This documentation covers the Smart Paathshala Payment API, which provides integration with multiple mobile financial services in Bangladesh, including bKash, Rocket, Tap, and Cellfin. The API allows educational institutions to manage student bill generation and payment processing through USSD (Unstructured Supplementary Service Data) channels.

## Base URL

```
https://backend.smartpathshalabd.com/api/v1
```

## Available Payment Providers

<div align="center">
  <table>
    <tr>
      <td align="center" width="25%">
        <a href="./bkash/BKASH_README.md">
          <img src="./assets/images/bkash-logo.png" alt="bKash Logo" width="200"><br>
          <strong>bKash</strong><br>
          Bangladesh's leading mobile financial service
        </a>
      </td>
      <td align="center" width="25%">
        <a href="./rocket/ROCKET_README.md">
          <img src="./assets/images/rocket-logo.png" alt="Rocket Logo" width="200"><br>
          <strong>Rocket</strong><br>
          Mobile banking service by Dutch-Bangla Bank
        </a>
      </td>
      <td align="center" width="25%">
        <a href="./tap/TAP_README.md">
          <img src="./assets/images/tap-logo.png" alt="Tap Logo" width="200"><br>
          <strong>Tap</strong><br>
          Digital payment solution for Bangladesh
        </a>
      </td>
      <td align="center" width="25%">
        <a href="./cellfin/CELLFIN_README.md">
          <img src="./assets/images/cellfin-logo.png" alt="Cellfin Logo" width="200"><br>
          <strong>Cellfin</strong><br>
          Mobile financial service for Bangladesh
        </a>
      </td>
    </tr>
  </table>
</div>

## Authentication

All API endpoints are secured with Basic Authentication. Each payment provider has its own set of credentials:

- **bKash**: Requires specific bKash Basic Auth credentials
- **Rocket**: Requires specific Rocket Basic Auth credentials
- **Tap**: Requires specific Tap Basic Auth credentials
- **Cellfin**: Requires specific Cellfin Basic Auth credentials

Basic Authentication credentials should be included in the headers of each request.

## Common Request Format

All endpoints accept form-data POST requests with a `data` parameter containing a JSON string with the required fields.

```http
POST /api/v1/invoices/ussd/{provider}/{endpoint} HTTP/1.1
Host: backend.smartpathshalabd.com
Authorization: Basic [encoded credentials]
Content-Type: multipart/form-data

data={
  "institute_id": "SPID9",
  "student_username": "SPID9",
  ...other parameters...
}
```

## Common Response Format

Most invoice/payment endpoints return a JSON response like this:

```json
{
  "statusCode": 200,
  "success": true,
  "message": "Retrieved successfully!",
  "data": {},
  "meta": null
}
```

Tap and Cellfin use provider-specific wrappers, but the invoice payloads are still documented in the provider READMEs below.

## Common Parameters

Most endpoints require the following parameters:

| Parameter          | Description                                                           |
| ------------------ | --------------------------------------------------------------------- |
| `institute_id`     | The unique identifier for the educational institution (e.g., "SPID9") |
| `student_username` | The unique identifier for the student (e.g., "SPID9")                 |

## Environment Variables

The API collection uses the following environment variables:

| Variable                   | Description                               |
| -------------------------- | ----------------------------------------- |
| `baseURL`                  | The base URL for the API                  |
| `basicAuthUsernameBkash`   | Username for bKash Basic Authentication   |
| `basicAuthPasswordBkash`   | Password for bKash Basic Authentication   |
| `basicAuthUsernameRocket`  | Username for Rocket Basic Authentication  |
| `basicAuthPasswordRocket`  | Password for Rocket Basic Authentication  |
| `basicAuthUsernameTap`     | Username for Tap Basic Authentication     |
| `basicAuthPasswordTap`     | Password for Tap Basic Authentication     |
| `basicAuthUsernameCellfin` | Username for Cellfin Basic Authentication |
| `basicAuthPasswordCellfin` | Password for Cellfin Basic Authentication |

## API Workflow

The Smart Paathshala Payment API follows this general workflow:

1. **Get Bill Information**: Retrieve bill details for a specific student
2. **Process Payment**: Record payment made through the mobile financial service
3. **Verify Payment Status**: Confirm if the payment was successful

## Invoice Response Shapes

The payment flow returns a small set of reusable invoice payloads:

```json
{
  "institute_id": "SPID9",
  "total_amount": "606",
  "student_name": "Abdullah Al MahMud",
  "student_username": "SPID9",
  "status": "Pending",
  "due_date": "20250724",
  "query_time": "20250717100015"
}
```

```json
{
  "institute_id": "SPID9",
  "student_name": "Abdullah Al MahMud",
  "student_username": "SPID9",
  "billing_month": "202507",
  "total_amount": "606",
  "user_wallet_number": "01773371221",
  "trxid": "TRX123456777",
  "pay_time": "20250717100055"
}
```

```json
{
  "institute_id": "SPID9",
  "student_name": "Abdullah Al MahMud",
  "student_username": "SPID9",
  "total_amount": "606",
  "trxid": "TRX123456777",
  "pay_time": "20250717100055"
}
```

Cellfin bill responses differ slightly and return `referenceId`, `dateTime`, `responseCode`, `responseMsg`, and `feeDetails`.

## Additional Resources

<div align="center">
  <table>
    <tr>
      <td align="center" width="25%">
        <a href="./bkash/BKASH_README.md">
          <img src="./assets/icons/documentation.png" alt="Documentation Icon" width="48"><br>
          <strong>bKash<br>Documentation</strong>
        </a>
      </td>
      <td align="center" width="25%">
        <a href="./rocket/ROCKET_README.md">
          <img src="./assets/icons/documentation.png" alt="Documentation Icon" width="48"><br>
          <strong>Rocket<br>Documentation</strong>
        </a>
      </td>
      <td align="center" width="25%">
        <a href="./tap/TAP_README.md">
          <img src="./assets/icons/documentation.png" alt="Documentation Icon" width="48"><br>
          <strong>Tap<br>Documentation</strong>
        </a>
      </td>
      <td align="center" width="25%">
        <a href="./cellfin/CELLFIN_README.md">
          <img src="./assets/icons/documentation.png" alt="Documentation Icon" width="48"><br>
          <strong>Cellfin<br>Documentation</strong>
        </a>
      </td>
    </tr>
  </table>
</div>

## Postman Collections

For testing the API endpoints, you can use the Postman collections provided in this repository:

- [bKash Postman Collection](./bkash/Bkash%20-%20Smart%20Paathshala%20Payment.postman_collection.json)
- [Rocket Postman Collection](./rocket/Rocket%20-%20Smart%20Paathshala%20Payment.postman_collection.json)
- [Tap Postman Collection](./tap/Tap%20-%20Smart%20Paathshala%20Payment.postman_collection.json)
- [Cellfin Postman Collection](./cellfin/Cellfin%20-%20Smart%20Paathshala%20Payment.postman_collection.json)

## Contact Information

For questions, support, or further information regarding this API documentation, please contact:

<div align="center">
  <table>
    <tr>
      <td align="center">
        <img src="./assets/icons/user.png" alt="Name Icon" width="24">
      </td>
      <td><strong>Name</strong></td>
      <td>Abdullah Al MahMud</td>
    </tr><tr>
      <td align="center">
        <img src="./assets/icons/netro-systems.png" alt="Company Icon" width="24">
      </td>
      <td><strong>Company</strong></td>
      <td><a href="https://netrosystems.com">Netro Systems</a></td>
    </tr>
    <tr>
      <td align="center">
        <img src="./assets/icons/email.png" alt="Email Icon" width="24">
      </td>
      <td><strong>Email</strong></td>
      <td><a href="mailto:abdudevs@gmail.com">abdudevs@gmail.com</a></td>
    </tr>
    <tr>
      <td align="center">
        <img src="./assets/icons/linkedin.png" alt="LinkedIn Icon" width="24">
      </td>
      <td><strong>LinkedIn</strong></td>
      <td><a href="https://www.linkedin.com/in/abdullahwins">Abdullah Al MahMud</a></td>
    </tr>
  </table>
</div>

<p align="center">
  <small>Last Updated: 2026-May-05</small>
</p>

<hr>

<p align="center">
  <small>© 2026 Smart Paathshala. All rights reserved.</small>
</p>
