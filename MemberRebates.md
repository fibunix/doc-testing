# Member Rebates — User Manual

## Overview

The Rebates extension gives members access to their rebate files. Members can view a list of rebate files, download them, and cancel files that haven't already been cancelled.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Members | View, download, and cancel rebate files |
| Store Admins | Manage rebate files in NetSuite file cabinet |
| Developers | Standard file list pattern with download and cancel actions |

## Usage Flows

### Viewing and Downloading Rebate Files

1. Navigate to "Rebates" in the Member Info menu
2. View the paginated list of rebate files (default 50 per page)
3. Sort files by name using the column header
4. Click the **Download** button on any file to save it to your computer

### Cancelling a Rebate File

1. In the rebate file list, locate the file you wish to cancel
2. Click the **Cancel** button (only visible if the file is not already cancelled)
3. A confirmation dialog appears: "Are you sure you want to cancel this file?"
4. Confirm to cancel — the file status changes to "Cancelled" and the list refreshes

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Records per page | List configuration | Number of files shown per page | 50 |

## Known Limitations & Edge Cases

- Files already in "Cancelled" status cannot be cancelled again (button is hidden)
- No search or date filtering is available on this page
- Only members can access this page — vendors are excluded
- Login is required

## Developer Notes

- Route: `/rebates`
- Member-only: checks `profile.isVendor === false`
- Uses standard file list pattern with `GlobalViews.Pagination` and `RecordViews.Actionable`
- Backend fetches from NetSuite file cabinet
- Cancel action sends POST to change file status
