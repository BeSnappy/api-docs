# Snappy API Documentation

## Introduction

All Snappy API end-points begin with `https://app.besnappy.com/api/v1/` and use the HTTPS protocol. All requests should also pass a username and password to authenticate via Basic Auth.

Response payloads are typically JSON; however, a few end-points return only a simple string identifier.

## Rate Limiting

The current Snappy API rate limit is 200 requests per minute.

## Endpoints

#### GET `/accounts`

Retrieve all of the accounts the authenticated account has access to.

```json
[
    {
        "id": 3,
        "organization": "Snappy Help",
        "domain": "help.besnappy.com",
        "plan_id": 1,
        "active": 1,
        "created_at": "2012-12-05 15:24:20",
        "updated_at": "2013-05-07 19:48:06",
        "custom_domain": ""
    }
]
```

#### GET `/account/{id}/mailboxes`

Retrieve all of the mailboxes attached to an account.

```json
[
    {
        "id": 3,
        "account_id": 3,
        "type": "email",
        "address": "hello@help.besnappy.com",
        "display": "Snappy Help",
        "auto_responding": 0,
        "auto_response": "",
        "active": 1,
        "created_at": "2012-12-05 15:24:20",
        "updated_at": "2013-04-18 18:10:43",
        "custom_address": null,
        "theme": "snappy",
        "local_part": "hello"
    }
]
```

#### GET `/account/{id}/staff`

Retrieve all of the staff attached to an account.

```json
[
    {
        "id": 3,
        "email": "ian@userscape.com",
        "sms_number": null,
        "first_name": "Ian",
        "last_name": "Landsman",
        "photo": null,
        "culture": "en",
        "notify": 1,
        "created_at": "2012-12-05 15:24:20",
        "updated_at": "2013-05-07 20:26:35",
        "signature": null,
        "tour_played": 1,
        "timezone": "America\/New_York",
        "notify_new": 1,
        "news_read_at": "2013-05-07 20:26:35",
        "username": "ian"
    }
]
```

#### GET `/mailbox/{id}/tickets`

Retrieve all of the **waiting** tickets from a mailbox.

```json
[
    {
        "id": 1,
        "account_id": 3,
        "mailbox_id": 3,
        "created_via": "email",
        "last_reply_by": "customer",
        "last_reply_at": 1368011747,
        "opened_by_staff_id": null,
        "opened_by_contact_id": 4,
        "opened_at": 1367934047,
        "status": "waiting",
        "first_staff_reply_at": "2013-05-07 13:41:06",
        "default_subject": "Re: Welcome to Snappy",
        "summary": "Message summary",
        "created_at": 1367934047,
        "updated_at": "2013-05-08 11:15:47",
        "unread": true,
        "tags": [
            "@ian"
        ],
        "contacts": [
            {
                "id": 4,
                "account_id": 3,
                "first_name": "John",
                "last_name": "Smith",
                "value": "john.smith@gmail.com",
                "provider": "email",
                "created_at": "2013-05-07 13:40:47",
                "updated_at": "2013-05-07 13:40:47",
                "type": "from"
            }
        ],
        "mailbox": {
        },
        "opener": {
            "id": 4,
            "account_id": 3,
            "first_name": "John",
            "last_name": "Smith",
            "value": "john.smith@gmail.com",
            "provider": "email",
            "created_at": "2013-05-07 13:40:47",
            "updated_at": "2013-05-07 13:40:47"
        }
    }
]
```

#### GET `/ticket/{id}`

Retrieve the details of a ticket.

```json
{
    "id": 1,
    "account_id": 3,
    "mailbox_id": 3,
    "created_via": "email",
    "last_reply_by": "customer",
    "last_reply_at": 1368011747,
    "opened_by_staff_id": null,
    "opened_by_contact_id": 4,
    "opened_at": 1367934047,
    "status": "waiting",
    "first_staff_reply_at": "2013-05-07 13:41:06",
    "default_subject": "Re: Welcome to Snappy",
    "summary": "Message summary",
    "created_at": 1367934047,
    "updated_at": "2013-05-08 11:15:47",
    "unread": true,
    "tags": [
        "@ian"
    ],
    "contacts": [
        {
            "id": 4,
            "account_id": 3,
            "first_name": "John",
            "last_name": "Smith",
            "value": "john.smith@gmail.com",
            "provider": "email",
            "created_at": "2013-05-07 13:40:47",
            "updated_at": "2013-05-07 13:40:47",
            "type": "from"
        }
    ],
    "mailbox": {
    },
    "opener": {
        "id": 4,
        "account_id": 3,
        "first_name": "John",
        "last_name": "Smith",
        "value": "john.smith@gmail.com",
        "provider": "email",
        "created_at": "2013-05-07 13:40:47",
        "updated_at": "2013-05-07 13:40:47"
    }
}
```

#### GET `/ticket/{id}/notes`

Get all of the notes attached to a ticket.

```json
[
    {
        "id": 102,
        "account_id": 3,
        "ticket_id": 11232,
        "created_by_staff_id": null,
        "created_by_contact_id": 4,
        "scope": "public",
        "created_at": 1368011747,
        "updated_at": "2013-05-08 11:15:47",
        "content": "Note content...",
        "contacts": [
            {
                "id": 4,
                "account_id": 3,
                "first_name": "John",
                "last_name": "Smith",
                "value": "john.smith@gmail.com",
                "provider": "email",
                "created_at": "2013-05-07 13:40:47",
                "updated_at": "2013-05-07 13:40:47",
                "type": "from"
            }
        ],
        "attachments": [
        ],
        "creator": {
            "id": 4,
            "account_id": 3,
            "first_name": "John",
            "last_name": "Smith",
            "value": "john.smith@gmail.com",
            "provider": "email",
            "created_at": "2013-05-07 13:40:47",
            "updated_at": "2013-05-07 13:40:47"
        }
    },
]
```

#### POST `/note`

Send a new note to one of the account's mailboxes.

#### POST `/ticket/{ticket}/tags`

Update the tags assigned to a ticket.

#### GET `/account/{id}/documents`

Retrieve all of the documents attached to an account.

#### GET `/account/{id}/document/{id}/download`

Download a document.

#### POST `/account/{id}/document`

Upload a document to the given account.

#### GET `/ticket/{id}/attachment/{id}/download`

Download an attachment.
