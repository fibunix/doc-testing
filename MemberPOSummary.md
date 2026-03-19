# Member PO Summary (Accounting Home) — User Manual

## Overview

The Accounting Home page is the member's financial dashboard. It displays an aging summary of accounts receivable, a PO balance overview, credit information, and a list of open purchase orders with the ability to close orders and export data to CSV.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Members | View financial overview, manage open purchase orders, download CSV reports |
| Store Admins | Purchase order and invoice data is pulled from NetSuite automatically |
| Developers | Dashboard extension combining summary widgets with a paginated PO list |

## Usage Flows

### Reviewing the Accounting Dashboard

1. Navigate to "Accounting Home" in the Accounting Center menu
2. The page displays four sections:

**Aging Summary Table** (top):
- Shows "As of: [today's date]" header
- Columns: Open Balance, Current, 1-30 Days, 31-60 Days, 61-90 Days, 91-120 Days, 120+ Days
- Each column amount is a clickable link that navigates to filtered invoices for that aging bucket
- All amounts formatted as currency

**Side Summary Card** (right):
- Purchases YTD (year-to-date total)
- Most Recent Activity (date)
- Last Payment (amount)
- Credit Limit (amount)

**PO Summary Section**:
- Total PO Balance
- Total A/R (Accounts Receivable)
- Total Credit
- Credit Available
- **Download** button to export PO data as CSV

### Downloading PO Data as CSV

1. On the Accounting Home page, click the **Download** button in the PO Summary section
2. A file named `purchase_orders.csv` downloads with columns:
   - PO# Date, Vendor, PO Total, Invoices Received, Invoices Total, Net PO Balance

### Closing a Purchase Order

1. In the Open Purchase Orders table, locate the order you want to close
2. Click the **Close Order** button in the Actions column
3. A confirmation dialog asks: "Are you sure you want to close this purchase order?"
4. Confirm to close — a success message appears: "The purchase order has been cancelled"
5. The list refreshes automatically

### Navigating to Invoice Details

1. In the Open Purchase Orders table, click a **Purchase Order #** link
2. You are navigated to the detailed view for that purchase order

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Records per page | List configuration | Number of open POs shown per page | 50 |
| Sort field | Table header | Sort by PO # or other columns | PO # |

## Known Limitations & Edge Cases

- Only **open** purchase orders are displayed in the table
- Aging summary amounts link to invoice views filtered by age bucket
- CSV export includes all PO data, not just the current page
- Close Order action is irreversible — confirmation is required
- Empty state: "You don't have any Open Purchase Orders at the moment"
- Only members can access this page — vendors are excluded

## Developer Notes

- Route: `/accounting-home`
- Member-only: checks `profile.isVendor === false`
- Reads Purchase Order records and linked Invoice records from NetSuite
- Aging data and credit information pulled from customer A/R data
- CSV generated client-side using PO collection data
- Uses `GlobalViews.Pagination` and `ListHeader` for sorting
