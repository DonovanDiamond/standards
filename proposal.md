
# Rules
- Always use camelCase to format field names. This is the standard for Java, Kotlin, Javascript and Go and many other languages.
- Required fields are *required* for the data to be loaded in the database or handled. Sometimes required fields may be missing while the data is being recorded or transferred but it may not be stored without the fields being present.
- All fields need to be escaped from any JSON, HTML, SQL, JavaScript, etc. injections when being recorded or sent to a database or interface.

# Required Fields

## Field: `source`
The source specifies what system recorded the information, regardless of the app:
- recorderv1

## Field: `application`
The system used to send/receive the data. A cellular phone call, even if recorded by the Signal app, would be the phone application but an SMS sent from Signal would not as Signal was responsible for sending it:
- signal
- phone
- whatsapp

## Field: `type`
The type of the data sent/received:
- text
- call
- sms
- mms

## Field: `direction`
The direction of the data from the device that recorded it:
- incoming
- outgoing

## Field: `originator`
The person who sent the data. This is not the contact or the chat, this would be the ID/Phone number of the device/email that sent the data or the device itself if it is outgoing.

Examples: `+123456789` or `mary@example.com`.

## Field: `recipient`
The id/number of where the data is being sent. This could be an ID of a group, or the phone number of a contact, or the id/number of the device if its incoming. 

Examples: `+123456789`, `whatsapp.group@12345` or `joe@example.com`.

## Field: `account`
The id/number of the device/account that recorded the information, this would be the device whether it is incoming or outgoing.

Examples: `+123456789` or `joe@example.com`.

## Field: `party`
> Party: A person or group participating in an action or affair.

The id/number of the remote person/group receiving and sending the information. This does not matter if its incoming or outgoing, it is always the other side.
Example: `+123` or `whatsapp.group@12345`, etc.

# Required field: `date`
The unix milisecond timestamp of the time the data was sent. This is preferrably when the message was sent from the originating device, although when that is not available, it can be the time received. Recording time sent and time received can be done, although should only be done in seperate custom fields.
Example: `1661169963237`
Rules:
- Must be unix miliseconds timestamp. Unix seconds timestamp can be `* 1000` to become miliseconds.

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
