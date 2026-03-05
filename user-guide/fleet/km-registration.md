---
title: "Km registration"
description: "Record and import kilometer readings for your trailers to track mileage over time."
---

The Km registration tab on the [[user-guide/fleet/trailer-details|trailer detail screen]] maintains a complete history of kilometer readings for each trailer. You can add readings manually or import them in bulk from an Excel file.

## Km registration list

The list displays all recorded readings in chronological order.

| Column | Description |
|--------|-------------|
| **Date** | Date when the reading was taken |
| **Km reading** | The odometer value recorded on that date |
| **Difference** | Kilometers driven since the previous reading |

## Adding a reading manually

### Step 1: Open the registration form

Click **Add reading** on the Km registration tab.

### Step 2: Enter the date and km value

Select the **Date** of the reading and enter the **Km reading** value.

### Step 3: Save the reading

Click **Save**. The difference from the previous reading is calculated automatically.


> [!warning]
> The km reading must be equal to or greater than the previous reading. The system rejects entries where the value decreases, as odometer readings cannot go backwards.


## Importing from Excel

For bulk entry, you can import km readings from an Excel file. This is useful when processing readings for multiple trailers at once.

### Step 1: Prepare your Excel file

Create an Excel file with three columns:

    | Column | Content |
    |--------|---------|
    | **Date** | The date of the reading |
    | **Plate number** | The trailer's license plate |
    | **Km** | The kilometer reading |

### Step 2: Upload the file

Click **Import from Excel** and select your file. ARMS reads the file and validates each row.

### Step 3: Review validation results

The system displays a summary of valid and invalid rows. Review any errors before confirming.

### Step 4: Confirm the import

Click **Confirm** to save all valid readings. Invalid rows are skipped and listed in the error summary.


### Import validation rules

Each row in the Excel file is validated against the following rules:

| Rule | Description |
|------|-------------|
| **Plate must exist** | The plate number must match an existing trailer in the system |
| **Date must be valid** | The date must be a valid calendar date |
| **Km must not decrease** | The km reading must be equal to or greater than the previous reading for that trailer |

> [!tip]
> If your import file contains readings for multiple trailers, each trailer's readings are validated independently. An error on one trailer does not affect readings for other trailers in the same file.


## Km chart

When sufficient data points exist, a line chart displays the km readings over time, giving you a visual overview of mileage trends for the trailer.

## Related pages

- **[[user-guide/fleet/trailer-details|Trailer details]]** — Access km registration from the trailer detail screen.

  - **[[user-guide/fleet/overview|Fleet overview]]** — Navigate to any trailer from the fleet list.
