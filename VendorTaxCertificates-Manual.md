# Vendor Tax Certificates — User Manual

## Overview

The Tax Certificates extension provides vendors with access to their tax certificate files. Vendors can search, download individual certificates, or bulk-download all certificates as a ZIP archive.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Vendors | Search, download, and bulk-download tax certificate files |
| Store Admins | Manage tax certificate files in NetSuite |
| Developers | File list with search and unique bulk ZIP download feature |

## Usage Flows

### Searching for Tax Certificates

1. Navigate to **Tax Certificates** in the My Account menu
2. Use the **search field** to find certificates by filename
3. Results update to show matching files
4. Click **Clear** to remove the search

### Downloading a Single Certificate

1. Browse or search for the desired certificate
2. Click the **Download** button on the file row
3. The file downloads to your computer

### Downloading All Certificates as ZIP

1. Click the **Download All** button (above the file list)
2. All certificates are packaged into a single ZIP file and downloaded

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Records per page | List configuration | Files shown per page | 50 |

## Known Limitations & Edge Cases

- **Read-only** — no upload, edit, or delete capabilities
- Search filters by filename only
- Download All creates a ZIP of all certificates, not just the current page
- Only vendors can access this page — members are excluded
- Login is required

## Developer Notes

- Route: `/tax-certificates`
- Vendor-only: checks `profile.isVendor === true`
- Backend: `services/BSP.Vendor_Tax_Certificates.Service.ss` (SS1.0)
- Bulk download: `action=download-all` parameter to service endpoint
- Caching enabled (`cacheSupport: true`)
