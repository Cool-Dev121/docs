---
order: 10
---

# REST API Authentication
The authentication with the REST API is a two step process.

1. Passing your username and password to the `/api/v1/login`
2. Using the `authToken` and `userId` provided back on every method

| Url | Short Description | Details Page |
| :--- | :--- | :--- |
| `/api/v1/login` | Authenticate with the REST API. | [Link](login.md) |
| `/api/v1/logout` | Invalidate your REST API authentication token. | [Link](logout.md) |
| `/api/v1/me` | Displays information about the authenticated user. | [Link](me.md) |
