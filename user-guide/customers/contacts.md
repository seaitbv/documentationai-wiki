---
title: "Contacts"
description: "Manage contact persons for your customers, including communication preferences and language settings."
---

Every customer in ARMS can have one or more contact persons. Contacts are used as recipients for offers, contracts, and invoices. The language assigned to a contact determines which template language is used when generating documents.

## Contact list

The contact list is displayed as a sub-table on the customer detail page. It shows the following columns:

| Column | Description |
|--------|-------------|
| **Name** | Full name of the contact person |
| **Language** | NL or FR |
| **Email** | Contact email address |
| **Phone** | Landline phone number |
| **Mobile** | Mobile phone number |
| **Communication** | Checkmark if this contact receives offers and contracts |
| **Invoicing** | Checkmark if this contact receives invoices and credit notes |

Click any contact row to open the contact detail form.

## Adding a contact

### Step 1: Open the customer detail page

Navigate to **Customers** and click the customer you want to add a contact to.

### Step 2: Click Add contact

In the **Contacts** section, click the **Add contact** button. The contact form opens with the **Customer** field pre-selected.

### Step 3: Fill in the contact details

Complete the contact form fields:

    | Field | Required | Description |
    |-------|----------|-------------|
    | **First name** | Yes | Contact's first name |
    | **Last name** | Yes | Contact's last name |
    | **Customer** | Yes | Pre-selected from the current customer. You can change this if needed. |
    | **Email** | No | Email address used for sending offers, contracts, and invoices |
    | **Phone** | No | Landline phone number |
    | **Mobile** | No | Mobile phone number |
    | **Language** | Yes | NL (Dutch) or FR (French) |
    | **For communication** | Yes | Check this box if the contact should receive offer and contract emails |
    | **For invoicing** | Yes | Check this box if the contact should receive invoices and credit notes |

### Step 4: Save the contact

Click **Save** to add the contact to the customer. The contact now appears in the contact list on the customer detail page.


## How contact language affects documents

The **Language** field on a contact is important because it determines the language used for generated documents:

- When you create an offer and select a contact, the **language** field on the offer is automatically set to the contact's language
- Document templates (offers, contracts) are generated in the contact's language
- Email body text sent via Outlook uses the language-specific template

> [!info]
> ARMS supports Dutch (NL) and French (FR). The contact's language is prefilled into offers and contracts but can be overridden per document if needed.


## Communication and invoicing flags

The two checkbox fields control which types of correspondence a contact receives:

| Flag | Purpose |
|------|---------|
| **For communication** | Contact receives offer emails, contract emails, and general correspondence |
| **For invoicing** | Contact receives invoices, credit notes, and payment reminders |

> [!tip]
> A single contact can have both flags enabled. For larger companies, you may want separate contacts for commercial communication and financial documents.


## Related pages

- **[[user-guide/customers/creating-customer|Creating a customer]]** — Add a new customer before creating contacts.

  - **[[user-guide/offers/creating-offer|Creating an offer]]** — Select a contact when creating an offer to prefill language settings.
