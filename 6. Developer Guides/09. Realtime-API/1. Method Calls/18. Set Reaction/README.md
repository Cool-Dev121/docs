# Set Reaction
Reacting to messages is a convenient way to "react" to messages with emojis, allowing for a wide variety of options for integrations, questions, and whatever else people can come up with.

## Requirements
| Logged In | Permission | Setting |
| --- | --- | --- |
| Yes | _none_ | _none_ |

## Example Call
Setting and removing a reaction requires a call to the same method with the same parameters. The first parameter is the reaction which is also the `emoji` and the second parameter is the message id of which the reaction is happening against.
```json
{
    "msg": "method",
    "method": "setReaction",
    "id": "22",
    "params": [
        ":nerd:",
        "messageId"
    ]
} 
```

## Example Response
```json
{
    "msg": "result",
    "id": "22"
}
```

## See Also
* [Reacting to Messages User Guide][1]

[1]:../../../4.%20User%20Guides/Reactions
