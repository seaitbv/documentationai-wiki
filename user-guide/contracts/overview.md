---
title: "Contract overview"
description: "View, filter, and manage all rental contracts from the contract list screen in ARMS."
---

The contract overview is your central hub for managing rental agreements. It displays all contracts in a searchable, filterable list with key information visible at a glance.

## Contract list columns

| Column | Description |
|--------|-------------|
| **Contract ID** | Auto-generated unique identifier |
| **Name** | The contract name |
| **Customer** | Customer name linked to the contract |
| **Trailer** | The trailer's display name (e.g., "K01 - QAMD180") |
| **Company** | The entity: Atrac or Urbain |
| **Start date** | Effective or estimated start date |
| **End date** | Effective or estimated end date |
| **Status** | Color-coded status badge |
| **Unit** | Billing unit: day, month, or km |

## Status badges

Each contract displays a color-coded badge indicating its current state:

| Status | Meaning |
|--------|---------|
| Created | Contract is drafted but not yet sent |
| Sent | Contract has been emailed to the customer |
| Accepted | Customer has accepted the contract |
| In rental | Rental period is active |
| To check | Trailer has been returned and awaits inspection |
| Completed | Inspection is done and contract is closed |
| Refused | Customer declined the contract |

> [!info]
> For the full lifecycle including automatic transitions and side effects, see [[user-guide/contracts/lifecycle|Contract lifecycle]].


## Default filter

By default, the list shows contracts in the statuses **In rental**, **Accepted**, and **To check**. These are the contracts that require active attention. You can expand the filter to include other statuses.

## Attention colors

The contract list uses yellow highlighting to flag contracts that need your attention:

| Highlight | Condition | Action needed |
|-----------|-----------|---------------|
| **Yellow row** | Contract is in "Sent" status for more than 7 days without a customer response | Follow up with the customer |
| **Yellow background** | Trailer has not been inspected after return, or damage has been found | Complete the [[user-guide/contracts/damage-control|damage control]] process |

> [!tip]
> Yellow-highlighted contracts also appear with the same color on the [[user-guide/planning/overview|planning timeline]], so you can spot them from multiple screens.


## Filtering the contract list

Use the filter bar above the list to narrow your results. You can combine multiple filters simultaneously.

| Filter | Options |
|--------|---------|
| **Status** | Multi-select: Created, Sent, Accepted, In rental, To check, Completed, Refused |
| **Company** | Atrac or Urbain |
| **Unit** | Day, Month, or Km |
| **Customer** | Search by customer name |
| **Search bar** | Searches by contract ID, name, or trailer |

## Actions

### Create a new contract

Click the **Add contract** button in the top-right corner to open the contract creation form. You can also create a contract directly from an accepted offer. See [[user-guide/contracts/creating-contract|Creating a contract]] for detailed steps.

### View contract details

Click any row in the contract list to open the full contract detail screen with all tabs (rental period, invoices, damage control, and more).

## Related pages

- **[[user-guide/contracts/creating-contract|Creating a contract]]** — Step-by-step guide to creating a new rental contract.

  - **[[user-guide/contracts/lifecycle|Contract lifecycle]]** — Understand the full status flow from creation to completion.
