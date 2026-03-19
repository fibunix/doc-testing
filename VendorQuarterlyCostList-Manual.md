# Vendor Quarterly Cost List — User Manual

## Overview

The Quarterly Cost List extension allows vendors to view quarterly cost list processing files, download them, and cancel files that are no longer needed.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Vendors | View, download, and cancel quarterly cost list files |
| Store Admins | Manage cost list files in NetSuite |
| Developers | File list with status tracking and cancel action |

## Usage Flows

### Viewing Quarterly Cost Files

1. Navigate to **Quarterly Cost-List Processing Files** in the My Account menu
2. The page displays a table with file name, status, and upload date
3. Use pagination to browse (default 50 per page)

### Downloading a File

1. Click the **Download** button on any file row
2. The file downloads to your computer

### Cancelling a File

1. Click the **Cancel** button on a file (only visible if the file is not already cancelled)
2. A confirmation dialog asks: "Are you sure you want to cancel this file?"
3. Confirm to cancel — the file status changes to "Cancelled"
4. The list refreshes automatically

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Records per page | List configuration | Files shown per page | 50 |

## Known Limitations & Edge Cases

- Files already in "Cancelled" status cannot be cancelled again — the button is hidden
- No search or date filtering available on this page
- Cancel action is confirmed before execution but is not reversible
- Only vendors can access this page — members are excluded
- Login is required

## Developer Notes

- Route: `/quarterly-cost`
- Vendor-only: checks `profile.isVendor === true`
- Backend: `services/Vendor_Quarterly_Cost_List.Service.ss` (SS1.0)
- Cancel sends POST with `internalid` to service endpoint
- `canCancel()` checks `status !== 'Cancelled'`
