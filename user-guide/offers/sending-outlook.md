---
title: "Sending via Outlook"
description: "How ARMS generates an offer PDF and creates an Outlook email draft for you to review and send."
---

ARMS integrates with Microsoft Outlook to streamline sending offers to customers. When you click the send button, the system generates a PDF, prepares an email draft with attachments, and opens it in Outlook for your review.

> [!warning]
> Sending offers via Outlook requires your Microsoft account to be connected to ARMS. Contact your administrator if the send button is not available.


## Send workflow

### Step 1: Open the offer

Navigate to the offer you want to send and open the offer detail page. The offer must be saved before you can send it.

### Step 2: Click Send by email

Click the **Send by email** button. ARMS begins preparing the email in the background.

### Step 3: System generates the offer PDF

ARMS fills in the selected template with the offer data (customer details, pricing, trailer properties, external description) and generates a PDF document.

### Step 4: System collects trailer photos

If a specific trailer is selected on the offer, the system retrieves all uploaded photos for that trailer. These are included as email attachments.

    > [!info]
> If no trailer is selected on the offer, this step is skipped and only the PDF is attached.

### Step 5: System creates an Outlook draft

ARMS uses the Microsoft Graph API to create an email draft in your Outlook mailbox with:

    | Element | Content |
    |---------|---------|
    | **Recipient** | Email address of the contact selected on the offer |
    | **Subject** | Configurable format, e.g., "Offer [ID] -- [Name] -- [Company]" |
    | **Body** | Standard text in the contact's language (configurable via [[user-guide/administration/parameters|Parameters]]) |
    | **Attachments** | Offer PDF + trailer photos (if applicable) |

    Outlook opens with the draft ready for review.

### Step 6: Review and send the email

Review the email in Outlook. You can edit the subject, body text, add CC recipients, or modify anything before sending. **You send the email yourself** from Outlook.

    > [!warning]
> ARMS does not send the email automatically. You have full control to review and modify the draft before sending.

### Step 7: Confirm sending

After clicking Send by email, ARMS displays a confirmation dialog: *"Was the email sent?"*

    - Click **Yes** to change the offer status from "Created" to **"Sent"**
    - Click **No** to keep the current status unchanged


> [!warning]
> ARMS cannot detect whether you actually sent the email in Outlook. The status change to "Sent" relies on your confirmation. Only click **Yes** if you have actually sent the email.


## Email body template

The default email body follows this structure (shown here in English for reference):

```
Dear [First name] [Last name],

Thank you for your interest in renting our trailer.
Please find the offer attached.

Kind regards,
The [Company] team
```

The actual text is configured per language (NL/FR) in the [[user-guide/administration/parameters|Parameters]] module. The language used matches the language set on the offer.

## Related pages

- **[[user-guide/offers/lifecycle|Offer lifecycle]]** — Understand how the "Sent" status fits into the overall offer flow.

  - **[[user-guide/offers/creating-offer|Creating an offer]]** — Prepare an offer before sending it to the customer.
