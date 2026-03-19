# Member Debit Memo Request — User Manual

## Overview

The Debit Memo Request extension allows members to request credits for returned products. Members search for an invoice, select line items to return, specify quantities and prices, choose a reason, and submit the request for processing by ISG headquarters.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Members | Search invoices, select items to return, submit debit memo requests |
| ISG Accounting (cash@isg.coop) | Receives and processes submitted debit requests |
| Developers | Multi-step form with invoice search, line item selection, and confirmation flow |

## Usage Flows

### Submitting a Debit Memo Request

1. Navigate to "Debit Memo Request" in the Accounting Center menu
2. Enter an invoice number in the search field (minimum 3 characters)
3. System searches for open invoices with remaining balance
4. Select an invoice from the results — invoice details card appears showing:
   - Supplier, Supplier Invoice #, Member #, ISG Invoice #, Invoice Date, PO #
5. Review the line items table with columns: Item Number, Description, Quantity, Price, Amount
6. Check the boxes next to items you want to return
7. For each selected item, adjust the rate/price if needed via the input field
8. Select a **Debit Reason** from the dropdown
9. Add optional comments (max 999 characters)
10. Review the **Total Credit Due** calculated at the bottom
11. Click Submit — a confirmation screen appears showing all selected items, quantities, rates, amounts, and total
12. Confirm the submission — request is sent to ISG for processing

### Confirmation

After successful submission, the confirmation page displays:
- "Thank you! Your request has been submitted."
- Debit requests are sent to cash@isg.coop for processing

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Debit reasons | Backend configuration | List of reasons available in the dropdown | Configured in NetSuite |
| Member number | `custentity_bsp_crm_cust_id` profile field | Displayed on invoice details card | From user profile |

## Known Limitations & Edge Cases

- Search requires a **minimum of 3 characters** to trigger
- Only invoices with a remaining balance are shown in search results
- Only invoices belonging to the current user are searchable
- At least one line item must be selected before submitting
- Comments field has a **999-character maximum**
- A debit reason must be selected — the form will not submit without one
- Confirmation modal appears before final submission to prevent accidental submissions

## Developer Notes

- Routes: `/debit-memo-request`, `/debit-memo-confirmation`
- Member-only: checks `profile.isVendor === false`
- Creates a Return Authorization record in NetSuite on submission
- Backend searches Invoice records and fetches line items
- Uses `custentity_bsp_crm_cust_id` custom field for member number display
