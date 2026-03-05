---
title: "Document templates"
description: "Upload, preview, and manage document templates used for generating offer and contract PDFs in ARMS."
---

The document templates module allows administrators to manage the templates used for generating offer and contract PDF documents. Each company (Atrac and Urbain) maintains separate templates for each language (NL and FR). This module is accessible only to users with the **Admin** role.

## How templates work

When ARMS generates a PDF for an offer or a contract, it uses a document template to format the output. The system selects the correct template based on:

1. **Company** -- Which entity the offer or contract belongs to (Atrac or Urbain)
2. **Document type** -- Whether it is an offer or a contract
3. **Language** -- The language of the contact person receiving the document

Each combination has a **default template** that the system uses automatically.

## Default templates per company

Each company has four default template slots:

| Template slot | Purpose |
|---------------|---------|
| **Default offer template (NL)** | Dutch offer PDF generation |
| **Default offer template (FR)** | French offer PDF generation |
| **Default contract template (NL)** | Dutch contract PDF generation |
| **Default contract template (FR)** | French contract PDF generation |

> [!info]
> The default templates are configured at the company level. When you set a template as default, it applies to all new documents generated for that company and language combination.


## Managing templates

### Uploading a new template

### Step 1: Open Template Management

Navigate to **Administration > Templates** in the main menu.

### Step 2: Select the company

Choose the company (Atrac or Urbain) for which you want to upload a template.

### Step 3: Choose the document type and language

Select whether the template is for an **offer** or a **contract**, and choose the language (**NL** or **FR**).

### Step 4: Upload the template file

Click **Upload** and select your template file. Templates can be in Word or HTML format.

    > [!warning]
> The maximum file size for uploads is controlled by the `MAX_UPLOAD_SIZE_MB` parameter (default: 25 MB). See [[user-guide/administration/parameters|Parameters]] for details.

### Step 5: Preview the template

After uploading, use the **Preview** function to render the template with sample data. Verify that the layout, formatting, and variable placeholders render correctly.

### Step 6: Set as default (optional)

If this template should be used for all new documents, click **Set as Default**. The previous default template is preserved but is no longer active.


### Previewing a template

The preview function renders a template with dummy data so you can verify the output before setting it as default. To preview:

1. Select the template from the list.
2. Click **Preview**.
3. Review the rendered output in the preview panel.

> [!tip]
> Always preview a template after uploading to verify that all placeholders resolve correctly and the formatting matches your expectations.


### Setting a default template

To change which template is used by default:

1. Select the template you want to activate.
2. Click **Set as Default**.
3. Confirm the change.

The previous default template remains in the system but is no longer used for new document generation. You can reactivate it at any time.

### Deactivating a template

To stop using a template without deleting it:

1. Select the template.
2. Click **Deactivate**.

Deactivated templates are preserved in the system for historical reference. They are not used for new document generation but remain visible in the template list.

> [!warning]
> Make sure another template is set as default before deactivating the current default. The system requires an active default template for each company, document type, and language combination.


## Template organization

The template list is organized by company and shows:

| Column | Description |
|--------|-------------|
| **Template name** | File name of the uploaded template |
| **Company** | Atrac or Urbain |
| **Document type** | Offer or Contract |
| **Language** | NL or FR |
| **Default** | Whether this is the active default template |
| **Upload date** | When the template was last uploaded |
| **Uploaded by** | User who uploaded the template |

## Related pages

- **[[user-guide/administration/parameters|System parameters]]** — Configure upload size limits and other system settings.

  - **[[user-guide/administration/dropdown-values|Dropdown values]]** — Manage dropdown field values used across ARMS.
