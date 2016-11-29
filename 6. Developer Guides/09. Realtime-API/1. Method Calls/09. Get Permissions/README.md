# Get Permissions

Use this call to get a collection with all the permissions of the server. Each permission will have the roles it applies to.

You may use this information to change your UI according to the permissons a user has (hidding what he can't do for example).

Example call:

```json
{
    "msg": "method",
    "method": "permissions/get",
    "id": "42",
    "params": []
}
```

Response:

```json
{
    "msg": "result",
    "id": "42",
    "result": [
        ... // permissions
    ]
}
```

## The Permisson object

The permission object describes a permisson as:

- `_id`: The permission's id
- `roles`: A collection of roles that this permissions applies to
- `_updatedAt`: (Optional) The last time this permission object was updated in the database
- `meta`: Metadata about the permission (described below)
- `$loki`: An internal property which can be ignored (it is removed on the web client before being added to the web client's database)

The `meta` object is defined as:

- `revision`: The revision of the permission
- `created`: Date the permission was created
- `version`: The permission version
- `updated`: (Optional) Date the permisson  was last updated

Example:

```json
{
    "_id": "snippet-message",
    "roles": [
        "owner",
        "moderator",
        "admin"
    ],
    "_updatedAt": { "$date": 1480377601 },
    "meta": {
        "revision": 3,
        "created": 1480377601,
        "version": 0,
        "updated": 1480377601
    },
    "$loki": 1
}
```
