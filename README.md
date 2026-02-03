# Flyt OAS One Roster API Documentation

This document provides comprehensive information about the One Roster API.

## Overview

The OneRoster API Gateway provides a unified interface for accessing educational roster data in compliance with the OneRoster standard. This includes details about academic sessions, classes, courses, enrollments, organizations and users.

## Getting Started

To use the One Roster API, follow these steps:

### 1. Obtain Client Credentials

- First, ensure you have a client set up in the [Visma developer's portal](https://oauth.developers.visma.com/service-registry/home). You can do this by contacting the Flyt Skole Support Team at skole@support.minflyt.no.
- Support will then be able to provide your unique `client_id` and `client_secret`
- These credentials must be kept secure since they are essential for your unique authentication.

### 2. Authentication

All endpoints require OAuth2 authentication using the Client Credentials flow. The API is integrated with Visma Connect for identity and access management.

#### Get an Access Token

Once you have your `client_id` and `client_secret`, you can obtain an access token by making a POST request to the Visma Connect token endpoint:

| Parameter        | Value                                     |
| ---------------- | ----------------------------------------- |
| **URL**          | `https://connect.visma.com/connect/token` |
| **Method**       | `POST`                                    |
| **Content-Type** | `application/x-www-form-urlencoded`       |

**Required Parameters:**

- `grant_type`: `client_credentials`
- `client_id`: `{your_client_id}`
- `client_secret`: `{your_client_secret}`
- `scope`: `one-roster-api:https://purl.imsglobal.org/spec/or/v1p2/scope/roster-core.readonly`

**Example Request:**
\`\`\`bash
curl -X POST https://connect.visma.com/connect/token \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "grant_type=client_credentials" \
  -d "client_id={your_client_id}" \
  -d "client_secret={your_client_secret}" \
  -d "scope=one-roster-api:https://purl.imsglobal.org/spec/or/v1p2/scope/roster-core.readonly"
\`\`\`

### 3. Call an API Endpoint

When you have an access token, you can call API endpoints.

| Parameter         | Value                                                        |
| ----------------- | ------------------------------------------------------------ |
| **URL**           | `https://api.oneroster.cloud.skole.visma.no/ims/oneroster/rostering/v1p2/orgs` |
| **Method**        | `GET`                                                        |
| **Authorization** | `Bearer {access_token}`                                      |

**Query Parameters:**

- `Limit`: `100` (maximum number of results)
- `Offset`: `0` (number of results to skip)

**Example Request:**
\`\`\`bash
curl -X GET "https://api.oneroster.cloud.skole.visma.no/ims/oneroster/rostering/v1p2/orgs?Limit=100&Offset=0" \
  -H "Authorization: Bearer {access_token}"
\`\`\`

### 4. Response Format

Responses are returned in JSON format following the OneRoster specification.

## API Documentation

Interactive documentation is available at the Swagger endpoint:

🔗 **[API Documentation](https://api.oneroster.cloud.skole.visma.no/swagger/index.html)**

You can explore all available endpoints and test them directly from the Swagger interface.

## Base URL

\`\`\`
https://api.oneroster.cloud.skole.visma.no/ims/oneroster/rostering/v1p2/
\`\`\`

## Common Endpoints

| Endpoint            | Description                |
| ------------------- | -------------------------- |
| `/orgs`             | Retrieve organizations     |
| `/schools`          | Retrieve schools           |
| `/courses`          | Retrieve courses           |
| `/classes`          | Retrieve classes           |
| `/users`            | Retrieve users             |
| `/enrollments`      | Retrieve enrollments       |
| `/academicSessions` | Retrieve academic sessions |

## Query Parameters

Most endpoints support the following query parameters:

- `limit`: Maximum number of results to return
- `offset`: Number of results to skip (for pagination)
- `filter`: Filter results based on specific criteria
- `sort`: Sort results by specified fields

## Error Handling

The API returns standard HTTP status codes:

- `200`: Success
- `400`: Bad Request
- `401`: Unauthorized
- `403`: Forbidden
- `404`: Not Found
- `500`: Internal Server Error

## Support

For additional support and questions, please refer to the Visme Flyt Support or (if you have access) to the Visma developer portal.

## OneRoster Specification v1.2

This API complies with the [IMS Global OneRoster v1.2 specification](https://www.imsglobal.org/sites/default/files/spec/oneroster/v1p2/rostering-restbinding/OneRosterv1p2RosteringService_RESTBindv1p0.html).
