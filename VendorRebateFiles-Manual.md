# Vendor Rebate Files — User Manual

## Overview

The Rebate Templates extension gives vendors access to browse and download rebate template files. This is a read-only listing — vendors cannot upload or modify files.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Vendors | Search, browse, and download rebate template files |
| Store Admins | Manage rebate template files in NetSuite file cabinet |
| Developers | Read-only file list with search and custom jQuery fetch |

## Usage Flows

### Searching for Rebate Templates

1. Navigate to File Processing > **Rebate Templates** in the My Account menu
2. Use the **search field** to find files by name
3. Results update to show matching files
4. Click **Clear** to remove the search and show all files

### Downloading a Rebate Template

1. Browse or search for the desired file
2. Click the **Download** button on the file row
3. The file downloads to your computer

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Records per page | List configuration | Files shown per page | 50 |

## Known Limitations & Edge Cases

- **Read-only** — no upload, edit, or delete capabilities
- Search filters by filename only
- Only one sort option: by filename
- Only vendors can access this page — members are excluded
- Login is required

## Developer Notes

- Route: `/rebate-templates`
- Vendor-only: checks `profile.isVendor === true`
- Menu: File Processing > Rebate Templates
- Backend: `services/BSP.VendorRebateFiles.Service.ss` (SS1.0)
- Uses custom jQuery.ajax fetch instead of Backbone sync
- Caching enabled (`cacheSupport: true`)
