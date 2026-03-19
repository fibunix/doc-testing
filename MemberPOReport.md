# Member PO Report (Purchase Summary Report) — User Manual

## Overview

The PO Report extension provides members with access to their Purchase Summary Report (PSR) files. Members can browse and download PSR files from a paginated list.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Members | Browse and download purchase summary report files |
| Store Admins | Manage PSR files in NetSuite file cabinet |
| Developers | Simple file list extension with download action only |

## Usage Flows

### Downloading a Purchase Summary Report

1. Navigate to "Purchase Summary Report (PSR)" in the Member Info menu
2. View the paginated list of PSR files
3. Sort files by name using the column header
4. Click the **Download** button on any file to save it to your computer

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Records per page | List configuration | Number of files shown per page | 50 |

## Known Limitations & Edge Cases

- This is a read-only file list — no upload, edit, or cancel capabilities
- No search or date filtering is available
- Only members can access this page — vendors are excluded
- Login is required
- Empty state message: "You don't have any Files at the moment, try adding one now!"

## Developer Notes

- Route: `/po-report`
- Member-only: checks `profile.isVendor === false`
- Uses standard file list pattern with pagination
- Backend fetches PSR files from NetSuite file cabinet
