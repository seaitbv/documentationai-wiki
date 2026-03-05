---
title: "Frequently Asked Questions"
description: "Answers to common questions about ARMS features, workflows, and business logic"
---

## General

> [!info] What is ARMS?
> ARMS (Atrac Rental Management System) is a web-based application for managing the complete trailer rental lifecycle. It covers fleet management, customer and contact administration, offer and contract workflows, invoicing with Exact Online integration, and visual planning.
>
>     ARMS serves two entities: **Atrac** (short to mid-term rental) and **Urbain** (long-term rental), both operating within the same software environment with separate templates, numbering, and VAT settings.


  > [!info]- Who can use ARMS?
> ARMS is available to authorized users within the Atrac/Urbain organization. Access is controlled through five roles:
>
>     - **Admin**: full access to all modules including system configuration
>     - **Commercial**: customer, offer, and contract management
>     - **Accounting**: invoice generation and Exact Online export
>     - **Fleet Manager**: trailer, inspection, and km management
>     - **Read-Only**: view access for management oversight
>
>     See the [[role-guides/by-role/admin|Role Guides]] for details on each role.


  > [!info]- What languages does ARMS support?
> ARMS supports **Dutch (NL)** and **French (FR)**. The interface language is determined by your user preference. Document templates (offers, contracts) exist in both languages per entity. The contact's language preference determines which template is used by default.
>
>     You can change your language at any time via the language switch in the header. See [[getting-started/logging-in|Logging In]] for details.


  > [!info]- How do I change my role or get access to a module I cannot see?
> Role assignments are managed by ARMS Administrators. If you need a different role or access to additional modules, contact your Administrator. They can update your role through user management.


  > [!info]- What is the difference between Atrac and Urbain?
> Atrac and Urbain are separate legal entities within the same organization:
>
>     - **Atrac** focuses on short to mid-term trailer rental.
>     - **Urbain** focuses on long-term trailer rental.
>
>     Both operate in the same ARMS instance but have separate templates, invoice numbering, and VAT settings. When creating offers and contracts, you select which entity is providing the rental.

## Offers

> [!info]- How do I send an offer to a customer?
> ARMS integrates with Microsoft Outlook to send offers:
>
>     1. Create and save the offer.
>     2. Click **Send via email** on the offer detail screen.
>     3. ARMS generates the offer PDF and opens an Outlook draft with the document attached.
>     4. Review, adjust if needed, and send from Outlook.
>     5. Confirm in ARMS that the email was sent.
>
>     The offer status changes to "Sent". See [[user-guide/offers/sending-outlook|Sending via Outlook]] for the complete process.


  > [!info]- What happens if VIES validation is unavailable?
> If the VIES service is temporarily unavailable when creating a customer, ARMS shows an orange warning: "VIES service temporarily unavailable -- fill in details manually."
>
>     You can:
>     - Fill in the company details manually and save the customer.
>     - Try the VIES check again later by clicking **Check VIES** on the customer detail screen.
>
>     The customer record is fully functional even without VIES validation. See [[user-guide/customers/vies-validation|VIES Validation]].


  > [!info]- Can I convert a rejected offer to a contract?
> No. Only offers with status **Accepted** can be converted to a contract. If a previously rejected offer needs to be revived, create a new offer (you can use the original offer as reference for the values).


  > [!info]- What is the offer due date and how is it calculated?
> The due date is the expiration date of the offer. It is automatically calculated as today + `OFFER_DUE_DATE_OFFSET_WEEKS` (default: 1 week). You can adjust the due date manually on each offer.
>
>     When the due date passes and the offer is still in "Created" or "Sent" status, it appears with a yellow badge in the overview and triggers a Dashboard notification.


  > [!info]- Do I need to select a trailer when creating an offer?
> No, the trailer is **optional** in the offer stage. You can specify desired trailer properties (type, volume, etc.) without selecting a specific trailer. The trailer becomes **required** when you convert the offer to a contract.
>
>     Selecting a trailer in the offer reserves it visually on the Planning timeline and allows trailer photos to be attached to the offer email.

## Contracts

> [!info]- How does the automatic 'In Rental' transition work?
> When a contract reaches **Accepted** status, ARMS runs a daily automated check. If the contract's effective start date (real start date, or estimated if real is not set) is today or in the past, the contract automatically transitions to **In Rental**.
>
>     This transition also:
>     - Creates a deposit invoice for the deposit amount
>     - Creates an advance invoice for the advance amount
>     - Changes the trailer status to "Rented"
>
>     See [[user-guide/contracts/lifecycle|Contract Lifecycle]] for all transitions.


  > [!info]- What are non-driving days?
> Non-driving days are periods during a **day-based** contract when the trailer is not in use (e.g., customer holidays). These days are deducted from the billable days when generating invoices.
>
>     Non-driving days only apply to day-based contracts. They do not affect month-based or km-based contracts.
>
>     ARMS monitors km registrations during non-driving periods. If average km per day exceeds the threshold (default: 10 km/day), the period is flagged in red.
>
>     See [[user-guide/contracts/non-driving-days|Non-Driving Days]].


  > [!info]- What is the 'invoice-to' customer field?
> The **invoice-to** field determines who receives the invoice for this contract. It defaults to the selected customer but can be changed to:
>
>     - **Atrac or Urbain**: for internal "commercial gestures" where the company absorbs part of the cost
>     - **STAS**: for warranty-covered rentals where the manufacturer pays
>
>     This allows flexibility in billing without changing the underlying customer relationship.


  > [!info]- How is the advance amount calculated?
> The advance amount is automatically calculated based on the contract's unit type:
>
>     | Unit | Formula |
>     |------|---------|
>     | Day | 30 x rental unit price |
>     | Month | 1 x rental unit price |
>     | Km | 6,000 x rental unit price |
>
>     The calculated amount is pre-filled but can be adjusted manually. The advance is invoiced automatically when the contract transitions to "In Rental" and is offset against the first recurrent invoice.
>
>     See [[user-guide/contracts/deposits-advances|Deposits & Advances]].

## Invoicing

> [!info]- How are forfait prices calculated for short rentals?
> For day-based contracts with a **total contract duration** of 1 or 2 days, ARMS applies fixed forfait pricing instead of the per-day rate:
>
>     | Duration | Forfait Price | Unit |
>     |----------|--------------|------|
>     | 1 day | 120 EUR (default) | per piece |
>     | 2 days | 170 EUR (default) | per piece |
>     | 3+ days | Normal day rate | per day |
>
>     The forfait amounts are configurable parameters (`FORFAIT_1_DAY_EUR` and `FORFAIT_2_DAYS_EUR`). The forfait is determined by the total contract duration, not the billing period length.
>
>     See [[user-guide/invoicing/day-based|Day-Based Invoicing]].


  > [!info]- What is anti-double-invoicing?
> Anti-double-invoicing is a built-in safety mechanism that prevents the same period or km range from being invoiced twice.
>
>     ARMS tracks:
>     - **Period locks**: for day and month contracts, recording which date ranges have been invoiced
>     - **Km locks**: for km contracts, recording which km ranges have been invoiced
>
>     When generating proposals, already-invoiced portions are automatically excluded and marked as "Partially invoiced" or "Fully invoiced" in the overview.
>
>     See [[user-guide/invoicing/proposals|Invoice Proposals]].


  > [!info]- How does the advance offset work on invoices?
> When the first recurrent invoice is generated for a contract, ARMS automatically adds a negative line to offset the advance payment:
>
>     1. The system checks the remaining advance balance (advance amount minus already offset amount).
>     2. If balance > 0, a "Advance offset" line is added with a negative amount.
>     3. The offset amount is the lesser of the remaining advance and the invoice subtotal.
>     4. Any remaining balance carries over to the next invoice.
>
>     This ensures the customer is not charged twice for the advance payment.


  > [!info]- How does month-based pro-rata calculation work?
> For month-based contracts that start or end mid-month:
>
>     1. ARMS calculates the number of active days in the month.
>     2. Divides by the total days in the month.
>     3. Rounds **up** to 2 decimal places.
>
>     **Example**: contract starts on February 26 in a 28-day month.
>     - Active days: 3 (26th, 27th, 28th)
>     - Fraction: 3/28 = 0.1071... rounded up = **0.11 months**
>     - Rental amount: 0.11 x unit price x (1 - discount%)
>
>     See [[user-guide/invoicing/month-based|Month-Based Invoicing]].

## Fleet

> [!info]- How do I register km readings?
> There are two methods:
>
>     **Manual entry:**
>     1. Open the trailer detail > **Km Registration** tab.
>     2. Click **Add Registration**.
>     3. Enter the date and km reading.
>     4. Save.
>
>     **Excel import:**
>     1. Click **Import from Excel** on the Km Registration tab.
>     2. Upload a file with columns for plate number, date, and km reading.
>     3. ARMS validates that plate numbers exist and km values are non-decreasing.
>
>     Km readings must always be greater than or equal to the previous reading for the same trailer. See [[user-guide/fleet/km-registration|Km Registration]].


  > [!info]- What are non-productive periods (NP periods)?
> Non-productive periods are times when a trailer is unavailable for rental. Common reasons include:
>
>     - **Damage**: trailer is being repaired
>     - **Inspection**: trailer is at the inspection center
>     - **Maintenance**: scheduled maintenance
>     - **Seasonal storage**: trailer stored during off-season
>
>     NP periods appear as grey blocks on the Planning timeline and cannot overlap with active contracts. See [[user-guide/fleet/non-productive-periods|Non-Productive Periods]].


  > [!info]- What are the critical trailer properties?
> Five properties are marked as "critical" because they are used to filter available trailers when creating offers and contracts:
>
>     1. **Trailer type** (Tipper/Walking floor/etc.)
>     2. **Volume** (m3)
>     3. **Sheet type** (tarpaulin type)
>     4. **Model**
>     5. **Door type**
>
>     Filling these in accurately ensures that Commercial users can find the right trailer for each customer's needs. See [[user-guide/fleet/trailer-details|Trailer Details]].

- **[[help/troubleshooting|Troubleshooting]]** — Solutions for common issues and error messages.

  - **[[help/glossary|Glossary]]** — Definitions of terms used throughout ARMS.
