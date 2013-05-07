# Snappy API Documentation

## Introduction

All Snappy API end-points begin with `https://app.besnappy.com/api/v1/` are use the HTTPS protocol. All requests should also pass a username and password via to authenticate via Basic Auth.

Response paylaods are typically JSON; however, a few end-points return only a simple string identifier.

## Rate Limiting

The current Snappy API rate limit is 200 requests per minute.

## Endpoints

#### GET `/accounts`

Retrieve all of the accounts the authenticated account has access to.

#### GET `/account/{id}/mailboxes`

Retrieve all of the mailboxes attached to an account.

#### GET `/account/{id}/staff`

Retrieve all of the staff attached to an account.

#### GET `/mailbox/{id}/tickets`

Retrieve all of the **waiting** tickets from a mailbox.

#### GET `/ticket/{id}`

Retrieve the details of a ticket.

#### GET `/ticket/{id}/notes`

Get all of the notes attached to a ticket.

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