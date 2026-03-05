---
title: "Troubleshooting"
description: "Solutions for common issues with login, email, VIES validation, invoicing, and document uploads in ARMS"
---

## Login issues

> [!info]- I cannot sign in with my Microsoft account
> **Possible causes and solutions:**
>
>     ### Step 1: Check your Microsoft account

>         Verify you are using the correct Microsoft account associated with your company. If you have multiple accounts, click "Use a different account" on the Microsoft login page.
>

### Step 2: Check your browser

>         Try clearing your browser cache and cookies, or open an incognito/private window. ARMS works best on the latest versions of Chrome, Edge, Firefox, and Safari.
>

### Step 3: Verify your account is provisioned

>         If this is your first time logging in, your ARMS Administrator must have provisioned your account. Contact them to confirm your account exists and has an assigned role.
>

### Step 4: Check Azure AD status

>         If multiple users cannot sign in, Azure Active Directory may be experiencing an outage. Check [Microsoft Service Health](https://status.cloud.microsoft) for current status.
>


  > [!info]- My session expired unexpectedly
> ARMS automatically logs you out after a period of inactivity. The default timeout is **60 minutes** but can be configured by your Administrator through the `SESSION_TIMEOUT_MINUTES` parameter.
>
>     **To resolve:**
>     1. Simply sign in again with your Microsoft account.
>     2. Any unsaved changes in forms will be lost. Save your work frequently.
>
>     > [!tip]
> > If sessions expire too quickly for your workflow, ask your Administrator to increase the `SESSION_TIMEOUT_MINUTES` parameter value.


  > [!info]- I see a 'No access' or 'Unauthorized' message after logging in
> This means your Microsoft account is authenticated but does not have an ARMS role assigned.
>
>     **To resolve:**
>     1. Contact your ARMS Administrator.
>     2. Ask them to assign you the appropriate role (Admin, Commercial, Accounting, Fleet Manager, or Read-Only).
>     3. Sign out and sign back in after the role is assigned.

## Email sending issues

> [!info]- The 'Send via email' button does not work or shows an error
> ARMS uses the Microsoft Graph API to create Outlook email drafts. Issues with this feature are typically related to Microsoft authentication.
>
>     ### Step 1: Check your Microsoft connection

>         Your Microsoft OAuth token may have expired. Try signing out of ARMS and signing back in. This refreshes the Microsoft connection.
>

### Step 2: Verify Outlook permissions

>         ARMS needs permission to create email drafts in your Outlook. If you see a "permissions" error, your Azure AD administrator may need to grant the required Microsoft Graph API permissions.
>

### Step 3: Check the contact email

>         Verify that the selected contact has a valid email address. If the contact's email field is empty, ARMS cannot create the draft.
>

### Step 4: Try again

>         If the issue is a temporary network or service problem, wait a moment and try again. Check [Microsoft Service Health](https://status.cloud.microsoft) if the problem persists.
>


  > [!info]- The offer/contract PDF is not attached to the email
> **Possible causes:**
>
>     - **Template is missing**: verify that an active template exists for the selected company, document type, and language. Contact your Administrator to check the [[user-guide/administration/templates|Templates]] configuration.
>     - **Template rendering error**: the template may contain invalid placeholders. Check the template preview to identify issues.
>     - **File size limit**: the generated PDF combined with attached photos may exceed email size limits. Try removing large photo attachments.


  > [!info]- Trailer photos are not attached to the offer email
> Trailer photos are only attached if:
>
>     1. A specific trailer is selected in the offer (not just desired properties).
>     2. The trailer has documents uploaded in its **Documents** tab.
>     3. The documents are categorized with a photo-related document type.
>
>     **To resolve:**
>     - Check that a trailer is selected in the offer.
>     - Open the trailer detail and verify photos are uploaded in the Documents tab.
>     - Ensure photos have the correct document type classification.

## VIES validation issues

> [!info]- VIES check returns 'Service temporarily unavailable'
> The European VIES service experiences periodic downtime for maintenance or high load. This is outside ARMS control.
>
>     **To resolve:**
>     1. Wait a few minutes and try again.
>     2. If urgent, fill in the customer details manually. You can re-run the VIES check later by clicking **Check VIES** on the customer detail screen.
>     3. Check [VIES service status](https://ec.europa.eu/taxation_customs/vies/) for known outages.
>
>     > [!info]
> > Manual entry is fully supported. The customer record functions normally even without VIES validation. You can validate later when the service is available.


  > [!info]- VIES check returns 'VAT number not found'
> **Common causes:**
>
>     - **Incorrect format**: ensure the VAT number includes the country prefix (e.g., BE0123456789, NL123456789B01).
>     - **New registration**: recently registered companies may take days or weeks to appear in VIES.
>     - **Inactive company**: the company may have been deregistered.
>
>     **To resolve:**
>     1. Double-check the VAT number format and digits.
>     2. Verify the VAT number with the customer.
>     3. If correct but not found, enter details manually and note the situation.

## Invoice generation issues

> [!info]- Invoice proposal shows 'Fully invoiced' for a contract I have not invoiced
> This means the period or km range for this contract has already been covered by a previous invoice.
>
>     **To investigate:**
>     1. Open the contract detail and go to the **Invoices** tab.
>     2. Check which invoices and periods/km ranges are already recorded.
>     3. The `Invoice_Period_Lock` and `Invoice_Km_Lock` records show exactly which ranges are covered.
>
>     If you believe this is an error, contact your Administrator to investigate the lock records.


  > [!info]- Invoice proposal shows a red row for a km-based contract
> A red row indicates **missing km registration data**. The last km reading for the trailer is older than the billing period end date.
>
>     **To resolve:**
>     1. Contact the Fleet Manager to register the current km reading.
>     2. Once the km reading is entered, re-generate the proposal.
>     3. The row should now show the correct driven km calculation.
>
>     > [!warning]
> > Do not create invoices from red rows. The calculated amount will be inaccurate due to missing km data.


  > [!info]- The advance offset line is not appearing on the first recurrent invoice
> The advance offset is only applied if:
>
>     1. An advance invoice was previously created for this contract (automatically generated when the contract transitions to "In Rental").
>     2. The advance amount has not been fully offset yet (remaining balance > 0).
>
>     **To check:**
>     - Open the contract's Invoices tab and look for the advance invoice.
>     - If no advance invoice exists, the contract may not have gone through the normal "Accepted to In Rental" transition.
>     - Contact your Administrator if the advance invoice is missing.


  > [!info]- Invoice totals do not match my manual calculation
> Common reasons for discrepancies:
>
>     - **Discount applies only to rental**, not insurance. Insurance lines are always at full price.
>     - **Insurance is always at 0% VAT**, regardless of the customer's VAT percentage.
>     - **Non-driving day deductions** reduce both rental and insurance lines (day-based contracts).
>     - **Forfait pricing** overrides the normal per-day calculation for 1-day and 2-day total contract durations.
>     - **Pro-rata rounding** for month-based contracts rounds up to 2 decimal places.
>
>     See the invoicing calculation guides: [[user-guide/invoicing/day-based|Day-Based]] | [[user-guide/invoicing/month-based|Month-Based]] | [[user-guide/invoicing/km-based|Km-Based]]

## Exact Online export issues

> [!info]- Export to Exact Online fails with an error
> ### Step 1: Read the error message

>         ARMS displays the error response from Exact Online. Common errors include:
>
>         - **Customer not found**: the customer's VAT number or code is not mapped in Exact Online. Add the customer in Exact Online first.
>         - **Invalid data**: a required field is missing or in the wrong format. Check the invoice details.
>         - **Authentication error**: the Exact Online API connection may have expired. Contact your Administrator.
>

### Step 2: Fix the underlying issue

>         Address the specific error:
>
>         - For customer mapping issues: create or update the customer in Exact Online.
>         - For data issues: review and correct the invoice details in ARMS.
>         - For authentication: the Administrator may need to re-authorize the Exact Online connection.
>

### Step 3: Retry the export

>         After fixing the issue, return to the invoice and click **Export to Exact Online** again. The invoice remains in "New" status until successfully exported.
>


  > [!info]- Invoice was exported but payment status is not updating
> Payment status synchronization from Exact Online may have a delay. If the status does not update:
>
>     1. Verify the invoice exists in Exact Online by checking the `exactonline_ref` field.
>     2. Check the payment status directly in Exact Online.
>     3. If the payment is recorded in Exact Online but not reflected in ARMS, contact your Administrator to investigate the sync mechanism.

## Document upload issues

> [!info]- File upload fails with 'File too large'
> The maximum upload size is controlled by the `MAX_UPLOAD_SIZE_MB` parameter (default: 25 MB).
>
>     **To resolve:**
>     - Compress the file (e.g., reduce image resolution or use PDF compression).
>     - Split large documents into multiple smaller files.
>     - If you regularly need larger uploads, ask your Administrator to increase the `MAX_UPLOAD_SIZE_MB` parameter.


  > [!info]- File upload fails with 'Unsupported format'
> ARMS supports the following file formats for document uploads:
>
>     - **PDF** (.pdf)
>     - **JPEG** (.jpg, .jpeg)
>     - **PNG** (.png)
>     - **TIFF** (.tif, .tiff)
>
>     **To resolve:**
>     - Convert your document to one of the supported formats.
>     - For Word documents, export to PDF first.
>     - For other image formats (BMP, GIF, WebP), convert to JPEG or PNG.


  > [!info]- Uploaded document does not appear in the list
> **Possible causes:**
>
>     - **Upload still processing**: large files may take a moment to process. Refresh the page after a few seconds.
>     - **Browser cache**: try a hard refresh (Ctrl+Shift+R or Cmd+Shift+R).
>     - **Upload failed silently**: check your network connection and try uploading again.
>     - **Permissions**: verify you have write access to the module (Read-Only users cannot upload documents).

## Still need help?

If your issue is not covered here:

1. Check the [[help/faq|FAQ]] for answers to common questions.
2. Review the relevant [[getting-started/introduction|User Guide]] section for detailed instructions.
3. Contact your ARMS Administrator for system-specific issues.

- **[[help/faq|FAQ]]** — Answers to frequently asked questions about ARMS.

  - **[[help/glossary|Glossary]]** — Definitions of terms used throughout ARMS.
