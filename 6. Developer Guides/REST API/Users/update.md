---
order: 50
---

# User Update
| URL | Requires Auth | HTTP Method |
| :--- | :--- | :--- |
| `/api/v1/users.update` | `yes` | `POST` |

## Payload
| Argument | Example | Required | Description |
| :--- | :--- | :--- | :--- |
| `userId` | `BsNr28znDkG8aeo7W` | Required | The id of the user to update. |
| `data.email` | `example@example.com` | Required | The email address for the user. |
| `data.name` | `Example User` | Required | The display name of the user. |
| `data.password` | `pass@w0rd` | Required | The password for the user. |
| `data.username` | `example` | Required | The username for the user. |
| `data.active` | `false` | Optional <br> Default: `true` | Whether the user is active, which determines if they can login or not. |
| `data.roles` | `['bot']` | Optional <br> Default: `['user']` | The roles the user has assigned to them. |
| `data.joinDefaultChannels` | `false` | Optional <br> Default: `true` | Whether the user should join the default channels. |
| `data.requirePasswordChange` | `true` | Optional <br> Default: `false` | Should the user be required to change their password when they login? |
| `data.sendWelcomeEmail` | `true` | Optional <br> Default: `false` | Should the user get a welcome email? |
| `data.verified` | `true` | Optional <br> Default: `false` | Should the user's email address be verified? |
| `data.customFields` | `{ twitter: '@example' }` | Optional <br> Default: `undefined` | Any custom fields the user should have on their account. |

## Example Call
```bash
curl -H "X-Auth-Token: 9HqLlyZOugoStsXCUfD_0YdwnNnunAJF8V47U3QHXSq" \
     -H "X-User-Id: aobEdbYhXfu5hkeqG" \
     -H "Content-type:application/json" \
     http://localhost:3000/api/v1/users.update \
     -d '{"userId": "BsNr28znDkG8aeo7W", "data": { "name": "new name", "email": "newemail@user.tld" }}'
```

## Example Result
```json
{
   "user":{
      "_id": "BsNr28znDkG8aeo7W",
      "createdAt": "2016-09-13T14:57:56.037Z",
      "services": {
         "password": {
            "bcrypt": "$2a$10$5I5nUzqNEs8jKhi7BFS55uFYRf5TE4ErSUH8HymMNAbpMAvsOcl2C"
         }
      },
      "username": "uniqueusername",
      "emails": [
         {
            "address": "newemail@user.tld",
            "verified": false
         }
      ],
      "type": "user",
      "status": "offline",
      "active": true,
      "roles": [
         "user"
      ],
      "_updatedAt": "2016-09-13T14:57:56.175Z",
      "name": "new name",
      "customFields": {
         "twitter": "userstwitter"
      }
   },
   "success": true
}
```

## Change Log
| Version | Description |
| :--- | :--- |
| 0.48.0 | Renamed to `users.update` | 
| 0.35.0 | Added as `user.update` |
