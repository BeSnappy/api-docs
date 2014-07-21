# Snappy API Documentation

## Introduction

All Snappy API end-points begin with `https://app.besnappy.com/api/v1/` and use the HTTPS protocol. All requests should also pass a username and password or API key to authenticate via Basic Auth.

You may retrieve your API key via the "Your Settings" menu in Snappy. Once in the settings menu, the security tab will provide access to your API key. When authenticating via API key, pass the key as the "username" and any string (such as "x) as the password.

Response payloads are typically JSON; however, a few end-points return only a simple string identifier.

## Rate Limiting

The current Snappy API rate limit is 200 requests per minute.

## Endpoints

- [Accounts](#accounts)
- [Search](#search)
- [Mailboxes](#mailboxes)
- [Staff](#staff)
- [Contacts](#contacts)
- [Waiting Tickets](#tickets)
- [Inbox Tickets](#inbox-tickets)
- [Your Tickets](#your-tickets)
- [Ticket Details](#ticket-details)
- [Ticket Notes](#ticket-notes)
- [Creating Tickets & Adding Notes](#adding-a-note)
- [Updating Ticket Tags](#updating-ticket-tags)
- [Documents](#documents)
- [Downloading Documents](#downloading-documents)
- [Downloading Attachments](#downloading-attachments)
- [Reading Team Wall](#reading-team-wall)
- [Posting To Team Wall](#posting-to-team-wall)
- [Deleting Wall Posts](#deleting-wall-posts)
- [Commenting On Wall Posts](#commenting-on-wall-posts)
- [Deleting Wall Comments](#deleting-wall-comments)
- [Liking Wall Posts](#liking-wall-posts)
- [Unliking Wall Posts](#unliking-wall-posts)
- [Searching FAQs](#searching-faqs)
- [Creating & Editing FAQs](#creating-and-editing-faqs)
- [Creating & Editing FAQ Topics](#creating-and-editing-topics)
- [Creating & Editing FAQ Questions](#creating-and-editing-questions)

<a name="accounts"></a>
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

<a name="search"></a>
#### GET `/account/{id}/search`

Perform a fuzzy search on an account's tickets.

Two items should be passed in the query string: `query` and `page`. The `query` parameter is your plain text search query. The `page` parameter allows you to indicate which page of results should be returned. Search results are returned with items for page.

In the search response, the `meta` property will give you the `total` amount of search results, not just the total for the current page.

```json
{
    "meta": {
        "total": 15,
        "page": 1
    },
    "data": [
        // Tickets found by the search...
    ]
}
```

<a name="mailboxes"></a>
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

<a name="staff"></a>
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

<a name="contacts"></a>
#### GET `/account/{id}/contacts/{id-or-email}`

Retrieve a contact associated with an account.

```json
[
    {
        "id": 1,
        "account_id": 1,
        "first_name": "Eugene",
        "last_name": "Haag",
        "value": "colleen.jenkins@example.com",
        "provider": "email",
        "created_at": "2013-12-02 14:55:27",
        "updated_at": "2013-12-02 14:55:27",
        "address": "colleen.jenkins@example.com"
    }
]
```

<a name="tickets"></a>
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

<a name="inbox-tickets"></a>
#### GET `/mailbox/{id}/inbox`

Retrieve all of the **new and unassigned** (inbox) tickets from a mailbox.

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

<a name="your-tickets"></a>
#### GET `/mailbox/{id}/yours`

Retrieve all of the **waiting** tickets that are assigned to you.

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

<a name="ticket-details"></a>
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

<a name="ticket-notes"></a>
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

<a name="adding-a-note"></a>
#### POST `/note`

Send a new note to one of the account's mailboxes. A ticket will automatically be created.

**Posting a note "from" a customer:**

```json
{
    "mailbox_id": 3,
    "subject": "Message Subject",
    "from": [
        {"name": "John Smith", "address": "john.smith@gmail.com"}
    ],
    "message": "Message Content"
}
```

**Posting a note "to" a customer:**

```json
{
    "mailbox_id": 3,
    "staff_id": 2,
    "subject": "Message Subject",
    "to": [
        {"name": "John Smith", "address": "john.smith@gmail.com"}
    ],
    "message": "Message Content"
}
```

To attach a note to an existing ticket, just add the ticket nonce to the payload in the `id` slot:

```json
{
    "id": "your-ticket-nonce",
    "mailbox_id": 3,
    "staff_id": 2,
    "subject": "Message Subject",
    "to": [
        {"name": "John Smith", "address": "john.smith@gmail.com"}
    ],
    "message": "Message Content"
}
```

To create a "private" note, set the scope on the JSON payload:

```json
{
    "id": "your-ticket-nonce",
    "mailbox_id": 3,
    "staff_id": 2,
    "subject": "Message Subject",
    "to": [
        {"name": "John Smith", "address": "john.smith@gmail.com"}
    ],
    "message": "Message Content",
    "scope": "private"
}
```

<a name="updating-ticket-tags"></a>
#### POST `/ticket/{id}/tags`

Update the tags assigned to a ticket.

The POST request should contain a `tags` field which contains a JSON encoded list of tags.

<a name="documents"></a>
#### GET `/account/{id}/documents`

Retrieve all of the documents attached to an account.

```json
[
    {
        "id": 60,
        "account_id": 3,
        "filename": "faq.png",
        "type": "image\/png",
        "size": 265420,
        "storage_key": "71be44f646d46af5023ec9dd21b732b4",
        "created_at": "2013-05-07 16:04:45",
        "updated_at": "2013-05-07 16:04:45"
    }
]
```

<a name="downloading-documents"></a>
#### GET `/account/{id}/document/{id}/download`

Download a document.

#### POST `/account/{id}/document`

Upload a document to the given account.

The document should be attached to the POST as a file named `document`. You may optionally include a POST field named `tags`. When included, the `tags` field should be a JSON encoded list of tags.

<a name="downloading-attachments"></a>
#### GET `/ticket/{id}/attachment/{attachment_id}/download`

Download an attachment.

<a name="reading-team-wall"></a>
#### GET `/account/{id}/wall`

Read the latest 25 posts from the team wall. You pass a wall post ID in the query string to "paginate" results:

`GET /account/{id}/wall?after=405

<a name="posting-to-team-wall"></a>
#### POST `/account/{id}/wall`

```json
{
    "content": "Post Content",
    "type": "post",
    "ticket": null,
    "note": null,
    "tags": ["foo", "bar"]
}
```

<a name="deleting-wall-posts"></a>
#### DELETE `/account/{id}/wall/{post_id}`

Delete a wall post.

<a name="commenting-on-wall-posts"></a>
#### POST `/account/{id}/wall/{post_id}/comment`

Comment on wall post. The comment content should be in a POST field named "content".

<a name="deleting-wall-comments"></a>
#### DELETE `/account/{id}/wall/{post_id}/comment/{comment_id}`

Delete a wall post comment.

<a name="liking-wall-posts"></a>
#### POST `/account/{id}/wall/{post_id}/like`

Like a given wall post.

<a name="unliking-wall-posts"></a>
#### DELETE `/account/{id}/wall/{post_id}/like`

Unlike a given wall post.

<a name="searching-faqs"></a>
### Searching FAQs

#### GET `/account/{id}/faqs/search?query=search&page=1`

```json
{  
   "meta":{  
      "total":2,
      "page":1
   },
   "data":[  
      {  
         "id":2,
         "account_id":1,
         "question":"Pricing and use of multiple accounts",
         "answer":"Snappy allows you to have multiple distinct accounts...",
         "created_at":"2014-07-21 20:22:12",
         "updated_at":"2014-07-21 20:22:12",
         "active":1
      },
      {  
         "id":1,
         "account_id":1,
         "question":"How do I use the custom contact lookup application?",
         "answer":"The custom contact application allows you to load...",
         "created_at":"2014-07-21 20:22:12",
         "updated_at":"2014-07-21 20:22:12",
         "active":1
      }
   ]
}
```

<a name="creating-and-editing-faqs"></a>
### Creating And Editing FAQs

#### GET `/account/{id}/faqs`

Get all of the FAQs for an account.

#### POST `/account/{id}/faqs`

Create a new FAQ.

Request:

```json
{
    "title": "My FAQ",
    "url": "faq"
}
```

#### PUT `/account/{id}/faqs/{faq_id}`

Update an FAQ.

Request:

```json
{
    "title": "My FAQ",
    "url": "faq"
}
```

#### DELETE `/account/{id}/faqs/{faq_id}`

Delete an FAQ.

<a name="creating-and-editing-topics"></a>
### Creating And Editing FAQ Topics

#### GET `/account/{id}/faqs/{faq_id}/topics`

Get all of the topics for an FAQ.

#### POST `/account/{id}/faqs/{faq_id}/topics`

Create a new FAQ topic.

Request:

```json
{
    "topic": "My topic name."
}
```

#### PUT `/account/{id}/faqs/{faq_id}/topics/{topic_id}`

Update an FAQ topic.

Request:

```json
{
    "topic": "My topic name."
}
```

#### DELETE `/account/{id}/faqs/{faq_id}/topics/{topic_id}`

Delete an FAQ topic.

<a name="creating-and-editing-questions"></a>
### Creating And Editing FAQ Questions

#### GET `/account/{id}/faqs/{faq_id}/topics/{topic_id}/questions`

Get all of the questions for a given topic.

#### POST `/account/{id}/faqs/{faq_id}/topics/{topic_id}/questions`

Create a new question for a topic.

```json
{
    "question": "My question.",
    "answer": "My answer."
}
```

#### PUT `/account/{id}/faqs/{faq_id}/topics/{topic_id}/questions/{question_id}`

Update a question.

```json
{
    "question": "My question.",
    "answer": "My answer."
}
```

#### PUT `/account/{id}/faqs/{faq_id}/topics/{topic_id}/questions/{question_id}/topics`

Update the topics a question is attached to.

```json
{
    "topics": [1, 2, 3]
}
```

#### DELETE `/account/{id}/faqs/{faq_id}/topics/{topic_id}/questions/{question_id}`

Delete a question.
