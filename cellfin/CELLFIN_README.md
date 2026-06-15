# Smart Paathshala Cellfin Payment Integration

This documentation covers the Cellfin payment integration for Smart Paathshala's payment system.

## Authentication

All Cellfin API endpoints require Basic Authentication with the following credentials:

```
Username: {{basicAuthUsernameCellfin}}
Password: {{basicAuthPasswordCellfin}}
```

These should be set as environment variables in your Postman environment or application configuration.

## Endpoints

### 1. Get Bill Information

Retrieves billing information for a student for a specific month.

**Endpoint:**

```
POST {{baseURL}}/invoices/ussd/cellfin/get-bill
```

**Request Parameters:**

```json
{
  "institute_id": "SPID9",
  "student_username": "SPID9",
  "billing_month": "202505"
}
```

| Parameter          | Type   | Description                                            |
| ------------------ | ------ | ------------------------------------------------------ |
| `institute_id`     | String | Unique identifier for the institution                  |
| `student_username` | String | Unique identifier for the student                      |
| `billing_month`    | String | Month for which the bill is requested (format: YYYYMM) |

**Example Request:**

```
POST /api/v1/invoices/ussd/cellfin/get-bill HTTP/1.1
Host: backend.smartpathshalabd.com
Authorization: Basic [encoded credentials]
Content-Type: multipart/form-data

data={
  "institute_id": "SPID9",
  "student_username": "SPID9",
  "billing_month": "202505"
}
```

**Response:**

```json
{
  "referenceId": "SPID9",
  "dateTime": "17/07/2025 10:00 AM",
  "responseCode": "00",
  "responseMsg": "SUCCESS",
  "feeDetails": {
    "studentId": "SPID9",
    "instituteName": "SPID9",
    "branchName": null,
    "shift": null,
    "className": "Class 10",
    "sectionName": null,
    "invoiceNo": "202505",
    "studentName": "Abdullah Al MahMud",
    "fatherName": "Abdur Rahman",
    "month": "May",
    "academicYear": "2025",
    "fee": 50,
    "waiver": null,
    "totalDue": 50
  }
}
```

### 2. Accept Payment

Records a payment made through Cellfin.

**Endpoint:**

```
POST {{baseURL}}/invoices/ussd/cellfin/accept-payment
```

**Request Parameters:**

```json
{
  "institute_id": "SPID9",
  "student_username": "SPID9",
  "billing_month": "202505",
  "total_amount": "50",
  "user_wallet_number": "01773371221",
  "trxid": "TRX123456781",
  "paid_at": "20250513033036"
}
```

| Parameter            | Type   | Description                                      |
| -------------------- | ------ | ------------------------------------------------ |
| `institute_id`       | String | Unique identifier for the institution            |
| `student_username`   | String | Unique identifier for the student                |
| `billing_month`      | String | Month for which payment is made (format: YYYYMM) |
| `total_amount`       | String | Amount paid (in Bangladeshi Taka)                |
| `user_wallet_number` | String | Cellfin wallet number used for payment           |
| `trxid`              | String | Unique transaction ID from Cellfin               |
| `paid_at`            | String | Payment timestamp (format: YYYYMMDDHHmmss)       |

**Example Request:**

```
POST /api/v1/invoices/ussd/cellfin/accept-payment HTTP/1.1
Host: backend.smartpathshalabd.com
Authorization: Basic [encoded credentials]
Content-Type: multipart/form-data

data={
  "institute_id": "SPID9",
  "student_username": "SPID9",
  "billing_month": "202505",
  "total_amount": "50",
  "user_wallet_number": "01773371221",
  "trxid": "TRX123456781",
  "paid_at": "20250513033036"
}
```

**Response:**

```json
{
  "responseCode": "00",
  "responseMsg": "success"
}
```

### 3. Check Payment Status

Checks the status of a payment using the transaction ID.

**Endpoint:**

```
POST {{baseURL}}/invoices/ussd/cellfin/check-payment-status
```

**Request Parameters:**

```json
{
  "institute_id": "SPID9",
  "trxid": "TRX123456789"
}
```

| Parameter      | Type   | Description                           |
| -------------- | ------ | ------------------------------------- |
| `institute_id` | String | Unique identifier for the institution |
| `trxid`        | String | Unique transaction ID to check        |

**Example Request:**

```
POST /api/v1/invoices/ussd/cellfin/check-payment-status HTTP/1.1
Host: backend.smartpathshalabd.com
Authorization: Basic [encoded credentials]
Content-Type: multipart/form-data

data={
  "institute_id": "SPID9",
  "trxid": "TRX123456789"
}
```

**Response:**

```json
{
  "statusCode": 200,
  "success": true,
  "message": "Retrieved successfully!",
  "data": {
    "institute_id": "SPID9",
    "student_name": "Abdullah Al MahMud",
    "student_username": "SPID9",
    "total_amount": "50",
    "trxid": "TRX123456789",
    "pay_time": "20250717100055"
  },
  "meta": null
}
```

## Integration Flow

1. **Get Bill Information**:
   - Call the `get-bill` endpoint to retrieve the bill amount for a student
   - Use the institute_id, student_username, and billing_month to identify the specific bill

2. **Process Payment**:
   - After user completes payment through Cellfin
   - Call the `accept-payment` endpoint with transaction details
   - Include all required parameters including trxid and paid_at timestamp

3. **Verify Payment Status**:
   - To check if a payment was successful
   - Call the `check-payment-status` endpoint with the institute_id and trxid

## Contact Information

For questions, support, or further information regarding this API documentation, please contact:

<div align="center">
  <table>
    <tr>
      <td align="center">
        <img src="../assets/icons/user.png" alt="Name Icon" width="24">
      </td>
      <td><strong>Name</strong></td>
      <td>Abdullah Al MahMud</td>
    </tr><tr>
      <td align="center">
        <img src="../assets/icons/netro-systems.png" alt="Company Icon" width="24">
      </td>
      <td><strong>Company</strong></td>
      <td><a href="https://netrosystems.com">Netro Systems</a></td>
    </tr>
    <tr>
      <td align="center">
        <img src="../assets/icons/email.png" alt="Email Icon" width="24">
      </td>
      <td><strong>Email</strong></td>
      <td><a href="mailto:abdudevs@gmail.com">abdudevs@gmail.com</a></td>
    </tr>
    <tr>
      <td align="center">
        <img src="../assets/icons/linkedin.png" alt="LinkedIn Icon" width="24">
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
