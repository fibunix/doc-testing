# Member Payment By Amount — User Manual

## Overview

The Payment By Amount extension allows eligible members to make a payment on their account without selecting specific invoices. Members enter a custom dollar amount, choose a payment date, provide credit/debit card details, and submit the payment through a guided 3-step wizard.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Members (with feature enabled) | Enter payment amount, select date, provide card details, submit payment |
| Store Admins | Enable/disable feature per customer via `custentity_bsp_pay_by_amount` field |
| Developers | 3-step payment wizard extending SCA's PaymentWizard module |

## Usage Flows

### Making a Payment by Amount

**Step 1 — Enter Amount** (`/pay-by-amount`)

1. Enter the dollar amount you wish to pay (minimum $0.01)
2. Optionally select a **Payment Date** (defaults to today, cannot be backdated)
3. The right sidebar shows a running payment summary with the formatted amount
4. Click **Continue** to proceed

**Step 2 — Payment & Review** (`/pay-by-amount-review`)

1. Select **Payment Method** (Credit / Debit Card)
2. Enter card details: card number, expiration date, CVV, cardholder name
3. Review the payment summary showing amount and payment date
4. Click **Submit** to process the payment
5. If 3D Secure authentication is required, a verification modal appears

**Step 3 — Confirmation** (`/pay-by-amount-confirmation`)

1. Confirmation page displays payment details: amount paid, payment date, payment method
2. Links available to return to your account

### Navigating Between Steps

- Use the **Back** button on Step 2 to return to Step 1 and modify the amount
- Values are preserved when navigating back
- Step progress indicator shows your current position in the wizard

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Feature flag | `custentity_bsp_pay_by_amount` on customer record | Must be set to `'T'` to enable for a customer | Not enabled |
| Transaction permission | NetSuite role permissions | `tranCustPymt` permission level must be >= 2 | Role-dependent |

## Known Limitations & Edge Cases

- This feature is **opt-in per customer** — the `custentity_bsp_pay_by_amount` field must be set to `'T'`
- Users without sufficient transaction permissions (`tranCustPymt < 2`) will see a forbidden error
- The amount must be greater than zero — entering $0 shows: "Please enter an amount greater than zero."
- Payment date cannot be set to a past date (minimum is today)
- This payment is **not tied to specific invoices** — it is a general account payment
- Only credit/debit card payments are supported (no ACH/bank transfer)
- 3D Secure authentication may be required depending on card issuer configuration
- Only members can access this page — vendors are excluded

## Developer Notes

- Routes: `/pay-by-amount`, `/pay-by-amount-review`, `/pay-by-amount-confirmation`
- Member-only: checks `profile.isVendor === false` AND `custentity_bsp_pay_by_amount === 'T'`
- Permission check: `SC.ENVIRONMENT.permissions.transactions.tranCustPymt >= 2`
- Extends SCA's `PaymentWizard` module with custom steps
- Creates a Customer Payment record in NetSuite
- Uses `LivePayment` model for payment processing
- Supports 3D Secure redirect flow if enabled
