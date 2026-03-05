---
title: "Exact Online export"
description: "Export invoices from ARMS to Exact Online for payment processing and accounting."
---

ARMS exports invoices to Exact Online, the accounting system used by both Atrac and Urbain. The current implementation uses a JSON file download that you upload to Exact Online. A direct API integration is planned for a future release.

## Prerequisites

Before you can export an invoice, ARMS validates the following:

| Requirement | Description |
|-------------|-------------|
| **Customer VAT number** | The customer must have a valid VAT number on their record |
| **Invoice number** | The invoice must have a generated invoice number |
| **Invoice date and due date** | Both dates must be set |
| **At least one invoice line** | The invoice must contain at least one line item |

> [!warning]
> If any validation fails, ARMS displays an error message explaining what is missing. Fix the issue on the invoice or customer record before retrying the export.


## Export process

### Step 1: Navigate to the invoice

On the [[user-guide/invoicing/managing-invoices|effective invoices]] tab, find the invoice you want to export. It must have the status "Created".

### Step 2: Click Export to Exact Online

Click the **Export to Exact Online** button. This button is only visible for invoices with the "Created" status.

### Step 3: Download the JSON file

ARMS validates the invoice data and generates a JSON file. The file downloads automatically to your computer.

### Step 4: Upload to Exact Online

Log in to Exact Online and upload the JSON file through the import interface. Follow your organization's Exact Online procedures for processing the import.

### Step 5: Verify the export

After a successful export, the invoice status in ARMS changes to "Sent". The Exact Online reference is stored on the invoice record.

    > [!info]
> If the export fails, ARMS displays the error response. Common issues include invalid VAT numbers or mismatched customer codes in Exact Online.


## Field mapping

ARMS maps invoice data to Exact Online fields as follows:

| ARMS field | Exact Online field | Notes |
|------------|-------------------|-------|
| Customer VAT number | `CustomerCode` | Used as the customer identifier in Exact Online |
| Invoice number | `YourRef` | The ARMS invoice number for cross-referencing |
| Invoice date | `InvoiceDate` | -- |
| Due date | `DueDate` | Calculated from payment conditions |
| Line description | `Description` | Per invoice line |
| Line quantity | `Quantity` | Per invoice line |
| Line unit price | `UnitPrice` | Per invoice line |
| Line net amount | `NetAmount` | Per invoice line |
| Line VAT rate | `VATCode` | Mapped using the table below |

### VAT code mapping

ARMS maps VAT percentages to Exact Online VAT codes:

| VAT % | Exact Online code |
|-------|-------------------|
| 21% | `1` |
| 12% | `3` |
| 6% | `2` |
| 0% | `0` |

> [!tip]
> Insurance lines always use VAT code `0` (0% VAT). Rental lines use the VAT code corresponding to the customer's VAT percentage.


## After export

Once an invoice is exported:

- The status changes from "Created" to **Sent**
- The Exact Online reference is stored on the invoice
- Payment status updates are returned from Exact Online (Open, Partially paid, Fully paid)
- You can view the Exact Online payment status on the [[user-guide/invoicing/managing-invoices|invoice list]]

## Future: direct API integration

A future release will replace the JSON download with a direct API integration using OAuth2 authentication. This will allow:

- Automatic export without manual file uploads
- Real-time payment status synchronization
- Automated reconciliation between ARMS and Exact Online

> [!info]
> Until the direct integration is available, continue using the JSON download workflow described above.


## Related pages

- **[[user-guide/invoicing/managing-invoices|Managing invoices]]** — View and manage all effective invoices and their statuses.

  - **[[user-guide/invoicing/overview|Invoicing overview]]** — Understand the full invoicing workflow in ARMS.
