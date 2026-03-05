---
title: "Customer server actions"
description: "Server actions for customer and contact CRUD operations with VIES VAT validation"
---

## Overview

The customer server actions in `lib/actions/customers.ts` handle CRUD operations for both customers and their contacts. This file also integrates with the EU VIES service for VAT number validation and address auto-fill.

## Input types

### CreateCustomerInput

```typescript
interface CreateCustomerInput {
  customer_name: string;
  vat_number?: string;
  official_name?: string;
  street?: string;
  number?: string;
  postal_code?: string;
  city?: string;
  country?: string;
  vat_percentage?: number;
  payment_conditions_id?: number;
  creditworthiness?: string;
}
```

### UpdateCustomerInput

```typescript
interface UpdateCustomerInput {
  customer_name?: string;
  vat_number?: string;
  official_name?: string;
  street?: string;
  number?: string;
  postal_code?: string;
  city?: string;
  country?: string;
  vat_percentage?: number;
  payment_conditions_id?: number | null;
  creditworthiness?: string;
  is_active?: boolean;        // Soft delete support
}
```

### CreateContactInput / UpdateContactInput

```typescript
interface CreateContactInput {
  customer_id: number;
  first_name: string;
  last_name: string;
  email?: string;
  phone?: string;
  mobile?: string;
  language?: "NL" | "FR";
  for_communication?: boolean;
  for_invoicing?: boolean;
}

interface UpdateContactInput {
  first_name?: string;
  last_name?: string;
  email?: string;
  phone?: string;
  mobile?: string;
  language?: "NL" | "FR";
  for_communication?: boolean;
  for_invoicing?: boolean;
}
```

## Customer functions

### getCustomer

| Property | Value |
|----------|-------|
| Signature | `getCustomer(customerId: number)` |
| Auth | None (public read) |
| Returns | `{ data: Record<string, any> \| null; error: string \| null }` |

### createCustomer

Creates a customer record with optional VAT uniqueness check.

| Property | Value |
|----------|-------|
| Signature | `createCustomer(input: CreateCustomerInput)` |
| Auth | `requireAuth()` |
| Returns | `{ data: { customer_id: number } \| null; error: string \| null }` |
| Revalidates | `/customers` layout |

**Validation:** `customer_name` required. If `vat_number` provided, must be unique (returns `DUPLICATE_VAT`).

### updateCustomer

| Property | Value |
|----------|-------|
| Signature | `updateCustomer(customerId: number, input: UpdateCustomerInput)` |
| Auth | `requireAuth()` |
| Returns | `{ error: string \| null }` |
| Revalidates | `/customers` layout |

### searchCustomers

Returns a list of active customers matching a search query, formatted for dropdown/lookup components.

| Property | Value |
|----------|-------|
| Signature | `searchCustomers(query: string)` |
| Auth | None |
| Returns | `{ value: string; label: string }[]` |
| Limit | 20 results |

## VIES functions

### checkViesVat

Thin wrapper around the `checkVies()` utility. Returns the raw VIES response.

| Property | Value |
|----------|-------|
| Signature | `checkViesVat(vatNumber: string)` |
| Returns | `ViesResponse` with status `"success"`, `"invalid"`, or `"unavailable"` |

### checkViesAndParse

Calls VIES and parses the returned address into structured fields (street, number, postal code, city, country). Used by the customer form to auto-fill address fields.

| Property | Value |
|----------|-------|
| Signature | `checkViesAndParse(vatNumber: string)` |
| Returns | `ViesParsedResult` |

```typescript
interface ViesParsedResult {
  status: "success" | "invalid" | "unavailable";
  official_name: string;
  street: string;
  number: string;
  postal_code: string;
  city: string;
  country: string;
  error: string | null;
}
```

## Contact functions

### getAllContacts

Fetches all contacts with their associated customer name, ordered by last name.

| Property | Value |
|----------|-------|
| Signature | `getAllContacts()` |
| Auth | None |
| Returns | Array of contact records with joined customer data |

### getContact

| Property | Value |
|----------|-------|
| Signature | `getContact(contactId: number)` |
| Auth | None |
| Returns | Single contact with customer join |

### getContacts

Fetches contacts belonging to a specific customer.

| Property | Value |
|----------|-------|
| Signature | `getContacts(customerId: number)` |
| Auth | None |
| Returns | Array of contacts for the customer |

### createContact

| Property | Value |
|----------|-------|
| Signature | `createContact(input: CreateContactInput)` |
| Auth | `requireAuth()` |
| Returns | `{ data: Record<string, any> \| null; error: string \| null }` |
| Revalidates | `/customers` and `/contacts` layouts |

**Validation:** `first_name` and `last_name` required. Defaults `language` to `"NL"` and booleans to `false`.

### updateContact

| Property | Value |
|----------|-------|
| Signature | `updateContact(contactId: number, input: UpdateContactInput)` |
| Auth | `requireAuth()` |
| Returns | `{ error: string \| null }` |
| Revalidates | `/customers` and `/contacts` layouts |

### deleteContact

Hard-deletes a contact record.

| Property | Value |
|----------|-------|
| Signature | `deleteContact(contactId: number)` |
| Auth | `requireAuth()` |
| Returns | `{ error: string \| null }` |
| Revalidates | `/customers` and `/contacts` layouts |
