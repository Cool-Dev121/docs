---
order: 17
---

# Get Integrations
Retrieves the integrations which the group has, requires the permission `manage-integrations`. It supports the [Offset, Count, and Sort Query Parameters](../Offset%20and%20Count%20and%20Sort%20Info.md) along with [Query and Fields Query Parameters](../Query%20and%20Fields%20Info.md).

| URL | Requires Auth | HTTP Method |
| :--- | :--- | :--- |
| `/api/v1/groups.getIntegrations` | `yes` | `GET` |

## Query Parameters
| Argument | Example | Required | Description |
| :--- | :--- | :--- | :--- |
| `roomId` | `ByehQjC44FwMeiLbX` | Required | The group's id |

## Example Call
```bash
curl -H "X-Auth-Token: 9HqLlyZOugoStsXCUfD_0YdwnNnunAJF8V47U3QHXSq" \
     -H "X-User-Id: aobEdbYhXfu5hkeqG" \
     http://localhost:3000/api/v1/groups.getIntegrations?roomId=ByehQjC44FwMeiLbX
```

## Example Result
```json
{
    "integrations": [{
        "_id": "WMQDChpnYTRmFre9h",
        "enabled": true,
        "username": "rocket.cat",
        "alias": "Guggy",
        "avatar": "http://res.guggy.com/logo_128.png",
        "name": "Guggy",
        "triggerWords": [
            "!guggy",
            "guggy",
            "gif+"
        ],
        "urls": [
            "http://text2gif.guggy.com/guggify"
        ],
        "token": "8DFS89DMKLWEN",
        "script": "const config = {\n    color: '#ffffff'\n};\n\nclass Script {\n    prepare_outgoing_request({ request }) {\n        const trigger = request.data.trigger_word + ' ';\n        const phrase = request.data.text.replace(trigger, '');\n        request.headers['Content-Type']='application/json';\n        request.headers['apiKey']=request.data.token;\n        return {\n            url: request.url,\n            headers: request.headers,\n            data: {format: 'gif', sentence: phrase},\n            method: 'POST'\n        };\n    }\n\n    process_outgoing_response({ request, response }) {\n        if(response.content.gif) {\n            return {\n                content: {\n                    attachments: [\n                        {\n                            image_url: response.content.gif,\n                            color: ((config['color'] != '') ? '#' + config['color'].replace('#', '') : '#ffffff')\n                        }\n                    ]\n                }\n            };\n        } else {\n            return {\n                content: {\n                    text: 'Sorry I don\\'t have a photo for you :disappointed_relieved:'\n                }\n            };\n        }\n    }\n}",
        "scriptEnabled": true,
        "impersonateUser": false,
        "scriptCompiled": "function _classCallCheck(instance,Constructor){if(!(instance instanceof Constructor)){throw new TypeError('Cannot call a class as a function')}}var config={color:'#ffffff'};var Script=function(){function Script(){_classCallCheck(this,Script)}Script.prototype.prepare_outgoing_request=function prepare_outgoing_request(_ref){var request=_ref.request;var trigger=request.data.trigger_word+' ';var phrase=request.data.text.replace(trigger,'');request.headers['Content-Type']='application/json';request.headers['apiKey']=request.data.token;return{url:request.url,headers:request.headers,data:{format:'gif',sentence:phrase},method:'POST'}};Script.prototype.process_outgoing_response=function process_outgoing_response(_ref2){var request=_ref2.request;var response=_ref2.response;if(response.content.gif){return{content:{attachments:[{image_url:response.content.gif,color:config['color']!=''?'#'+config['color'].replace('#',''):'#ffffff'}]}}}else{return{content:{text:'Sorry I don\\'t have a photo for you :disappointed_relieved:'}}}};return Script}();",
        "scriptError": null,
        "type": "webhook-outgoing",
        "userId": "rocket.cat",
        "channel": [
            "#private-group-name"
        ],
        "_createdAt": "2017-01-05T17:06:05.660Z",
        "_createdBy": {
            "username": "graywolf336",
            "_id": "R4jgcQaQhvvK6K3iY"
        },
        "_updatedAt": "2017-01-05T17:06:05.660Z"
    }],
    "success": true
}
```

## Change Log
| Version | Description |
| :--- | :--- |
| 0.49.0 | Added |
