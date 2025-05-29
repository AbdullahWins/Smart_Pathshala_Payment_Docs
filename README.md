# Smart Paathshala Payment API Documentation

## Overview

This documentation covers the Smart Paathshala Payment API, which provides integration with multiple mobile financial services in Bangladesh, including bKash and Rocket. The API allows educational institutions to manage student bill generation and payment processing through USSD (Unstructured Supplementary Service Data) channels.

## Base URL

```
https://backend.smartpathshalabd.com/api/v1
```

## Available Payment Providers

- [bKash](./BKASH_README.md) - Bangladesh's leading mobile financial service
- [Rocket](./ROCKET_README.md) - Mobile banking service by Dutch-Bangla Bank

## Authentication

All API endpoints are secured with Basic Authentication. Each payment provider has its own set of credentials:

- **bKash**: Requires specific bKash Basic Auth credentials
- **Rocket**: Requires specific Rocket Basic Auth credentials

Basic Authentication credentials should be included in the headers of each request.

## Common Request Format

All endpoints accept form-data POST requests with a `data` parameter containing a JSON string with the required fields.

## Common Parameters

Most endpoints require the following parameters:

- `institute_id`: The unique identifier for the educational institution (e.g., "SPID9")
- `student_username`: The unique identifier for the student (e.g., "SPID9")

## Environment Variables

The API collection uses the following environment variables:

- `baseURL`: The base URL for the API
- `basicAuthUsernameBkash`: Username for bKash Basic Authentication
- `basicAuthPasswordBkash`: Password for bKash Basic Authentication
- `basicAuthUsernameRocket`: Username for Rocket Basic Authentication
- `basicAuthPasswordRocket`: Password for Rocket Basic Authentication

## Additional Resources

- [bKash Payment Documentation](./BKASH_README.md)
- [Rocket Payment Documentation](./ROCKET_README.md)


## Contact Information

For questions, support, or further information regarding this API documentation, please contact:

- **Name**: Abdullah Al MahMud
- **Email**: abdudevs@gmail.com
- **LinkedIn**: [https://www.linkedin.com/in/abdullahwins](https://www.linkedin.com/in/abdullahwins)
- **GitHub**: [https://github.com/AbdullahWins](https://github.com/AbdullahWins)

Last Updated: 2025-05-29
