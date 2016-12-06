# Delete Message

There is only way one to delete a message inside of Rocket.Chat, but it only requires the message's `_id` being passed in.

## Requirements
| Logged In | Permission | Setting |
| --- | --- | --- |
| Yes | `delete-message` | `Message_AllowDeleting` - "Allow Message Deleting" |

## Example Call
All that is needed to delete a message is passing the `_id` of the message.
```json
{
    "msg": "method",
    "method": "deleteMessage",
    "id": "42",
    "params": [ { "_id": message_id } ]
} 
```

## Example Response
```json
{
    "msg": "result",
    "id": "42",
    "result": []
}
```

## Additional Information
As mentioned in requirements, you must be logged in to be able to delete a message along with having the permission `delete-message`. Two settings apply, `Message_AllowDeleting` and then `Message_AllowDeleting_BlockDeleteInMinutes`. The first setting is a boolean, true/false, and the second setting is an integer that can be `0` for always being allowed to delete or it can be greater than zero which the deleting with be disallowed/blocked after the time has passed.

## See Also
* [Send Message Method][1]
* [Update Message Method][2]

[1]:../12.%20Send%20Message
[2]:../13.%20Update%20Message