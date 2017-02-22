---
order: 5
---

# Livechat API

## Usage

Livechat API code must be inserted after the livechat installation script and wrapped as a callback of `RocketChat();` function.

You can call multiple livechat APIs on the same page.

### Methods

#### *Set custom field*
To set a custom field for a visitor, you can use the following code:

```javascript
RocketChat(function() {
    this.setCustomField('fieldName1', 'Any value you want to store');
    this.setCustomField('fieldName2', 'A value set just once', false); // you can pass false as the third parameter to not overwrite an already set value
});
```

#### *Set theme options*
To change the online color of the livechat widget, use the following code:

```javascript
RocketChat(function() {
    this.setTheme({
        color: '#04436A', // widget title background color
        fontColor: '#FFFFFF' // widget title font color
    });
});
```

### Events

#### _onChatMaximized_
Fired when the chat widget is maximized.

```javascript
RocketChat(function() {
    this.onChatMaximized(function() {
        // do whatever you want
        console.log('chat widget maximized');
    });
});
```

#### _onChatMinimized_
Fired when the chat widget is minimized.

```javascript
RocketChat(function() {
    this.onChatMinimized(function() {
        // do whatever you want
        console.log('chat widget minimized');
    });
});
```

#### _onChatStarted_
Fired when the chat is started (the first message was sent).

```javascript
RocketChat(function() {
    this.onChatStarted(function() {
        // do whatever you want
        console.log('chat started');
    });
});
```

#### _onChatEnded_
Fired when the chat is ended either by the agent or the visitor.

```javascript
RocketChat(function() {
    this.onChatEnded(function() {
        // do whatever you want
        console.log('chat ended');
    });
});
```

#### _onPrechatFormSubmit_
Fired when the pre-chat form is submitted.

```javascript
RocketChat(function() {
    this.onPrechatFormSubmit(function(data) {
        // data is an object containing the following fields: name, email and deparment (the department _id)

        // do whatever you want
        console.log('pre-chat form submitted');
    });
});
```

#### _onOfflineFormSubmit_
Fired when the offline form is submitted.

```javascript
RocketChat(function() {
    this.onOfflineFormSubmit(function(data) {
        // data is an object containing the following fields: name, email and message

        // do whatever you want
        console.log('offline form submitted');
    });
});
```

## Change Log
| Version | Description |
| :--- | :--- |
| 0.53.0 | Added callback events and the ability to pass a flag to `setCustomField` so the value passed does not get wrote if there is already an existing value. |
| 0.36.0 | Added `setTheme` method |
| 0.26.0 | Added `setCustomField` method |
