
# Rules
Always use camelCase to format field names. This is the standard for Java, Kotlin, Javascript and Go and many other languages.

# Rquired field: `source`
The source specifies what system recorded the information, regardless of the app:
- <>
- <>
- <>
- <>

# Required field: `application`
The system used to send/receive the data. A cellular phone call, even if recorded by the Signal app, would be the phone application but an SMS sent from Signal would not as Signal was responsible for sending it:
- signal
- phone
- whatsapp

# Required field: `type`
The type of the data sent/received:
- text
- call
- sms
- mms

# Required field: `direction`
The direction of the data from the device that recorded it:
- incoming
- outgoing

# Required field: `originator`
The person who sent the data. This is not the contact or the chat, this would be the ID/Phone number of the person who sent the data or the device if it is outgoing.
Example, `+123`.

# Required field: `recipient`
The id/number of where the data is being sent. This could be an ID of a group, or the phone number of a contact, or the id/number of the device if its incoming.
Example: `+123` or `whatsapp.group@12345`, etc.

# Required field: `user`
> User: One who uses a computer, computer program, or online service.

The id/number of the device that recorded the information, this would be the device whether it is incoming or outgoing.
Example: `+123`.

# Required field: `party`
> Party: A person or group participating in an action or affair.

The id/number of the remote person/group receiving and sending the information. This does not matter if its incoming or outgoing, it is always the other side.
Example: `+123` or `whatsapp.group@12345`, etc.

# Required field: `date`


# Required field: `content`
The data that was sent or received. This is an object which contains information as this can change depending on the type of data sent or received.
Example:
```json
{
    "type": "text",
    "content": {
        "body": "hi there",
    }
},{
    "type": "call",
    "content": {
        "duration": 132
    }
},{
    "type": "call",
    "content": {
        "duration": 0,
        "type": "missed"
    }
},{
    "type": "text",
    "content": {
        "body": "this is awesome",
        "attachments": ["87216371263.jpeg"]
    }
},{
    "type": "text",
    "content": {
        "body": "no it doesnt",
        "referredMessage": {
            "type": "text",
            "content": {
                "body": "does it work?"
            }
        }
    }
}
```
