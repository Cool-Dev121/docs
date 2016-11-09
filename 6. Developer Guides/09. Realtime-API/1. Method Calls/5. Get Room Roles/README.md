# Get Room Roles

This method call is used to get room-wide special users and their roles. You may send an collection of room id (at least one).

The `result` is a collection of users and its roles per room.

The user roles per room object is defined as:

- `rid`: The room id this user and role belongs to
- `u`: A simple user object with the user id and username
- `roles`: The collection of roles of the user in the room
- `_id`: the id of this object

Example call:

```json
{
    "msg": "method",
    "method": "getRoomRoles",
    "id": "42",
    "params": [ "room-id" ]
}
```

Response:

```json
{
    "msg": "result",
    "id": "42",
    "result": [
        {
            "rid": "room-id",
            "u": { "_id": "user-id", "username": "username" },
            "roles": [ "role-name" ],
            "_id": "id"
        }
    ]
}
```
