---
title: "Sending a contract via Outlook"
description: "Send a contract to the customer via Microsoft Outlook email integration in ARMS."
---

ARMS integrates with Microsoft Outlook to let you send contract documents directly from the application. When you send a contract, the status changes from "Created" to "Sent".

## What gets sent

When you send a contract via email, the following items are attached:

| Attachment | Description |
|------------|-------------|
| **Contract PDF** | The completed contract document generated from the selected template |
| **Trailer registration document** | The trailer's official registration certificate (inschrijvingsbewijs) |

> [!info]
> Make sure the trailer's registration document is uploaded in the [[user-guide/fleet/documents|trailer documents]] section before sending the contract. If it is missing, you need to upload it first.


## Sending a contract

### Step 1: Open the contract

Navigate to the contract detail screen from the [[user-guide/contracts/overview|contract overview]].

### Step 2: Review the contract document

On the **Contract visualization** tab, preview the generated PDF to make sure all details are correct.

### Step 3: Click Send via email

Click the **Send via email** button. ARMS opens a dialog with the email details.

### Step 4: Review the email

The dialog shows:
    - **Recipient**: The contact's email address (from the contract header)
    - **Subject**: Pre-filled based on the contract template
    - **Body**: Default email text in the contact's language (see below)
    - **Attachments**: Contract PDF and trailer registration document

    You can edit the subject and body text before sending.

### Step 5: Confirm and send

Click **Send** to dispatch the email via Outlook. After confirmation, the contract status changes to "Sent".


## Default email text

The email body is pre-filled based on the contact's language setting. The default text asks the customer to review and return the signed contract.

> [!tip]
> The default email text per language is configurable in [[user-guide/administration/parameters|Parameters]]. Your administrator can customize the text templates for both Dutch and French.


## After sending

Once the contract is sent:

- The status changes to **Sent** and cannot be reverted to "Created"
- The contract appears in the list with the "Sent" badge
- If the customer does not respond within 7 days, the contract row turns **yellow** in the [[user-guide/contracts/overview|contract overview]] as a follow-up reminder
- You can manually update the status to **Accepted** or **Refused** based on the customer's response

## Related pages

- **[[user-guide/contracts/lifecycle|Contract lifecycle]]** — See all status transitions and what happens after sending.

  - **[[user-guide/contracts/overview|Contract overview]]** — Monitor sent contracts and follow up on yellow-highlighted ones.
