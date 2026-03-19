# Vendor Submit Invoice — User Manual

## Overview

The Submit Invoice extension allows vendors to upload Excel invoice files to ISG, browse previously submitted invoices, filter by date, and download files.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Vendors | Upload invoice files, browse submitted invoices, download files |
| ISG Staff | Process received invoice files |
| Developers | File upload extension with date filtering and pagination |

## Usage Flows

### Uploading an Invoice File

1. Navigate to Supplier Info > **Submit Invoice** in the My Account menu
2. Click the **Upload** button to open the upload modal
3. Select an Excel file (.xlsx or .xls) — maximum 10 MB
4. Optionally add a description
5. Click **Upload** — a progress bar shows upload progress
6. On success, the modal closes and the file list refreshes

### Browsing Submitted Invoices

1. View the file list sorted by filename (default) or creation date
2. Use the **Date Received** filter to show files from a specific date
3. Click **Clear** to remove the date filter
4. Navigate through pages using pagination controls (default 50 per page)

### Downloading an Invoice File

1. Click the **Download** button on any file row
2. The file downloads to your computer

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Records per page | List configuration | Files shown per page | 50 |

## Known Limitations & Edge Cases

- Only **Excel files** (.xlsx, .xls) are accepted
- Maximum file size is **10 MB**
- All uploaded files are automatically classified as type "invoice"
- Only vendors can access this page — members are excluded
- Login is required

## Developer Notes

- Route: `/submit-invoice`
- Vendor-only: checks `profile.isVendor === true`
- Menu: Supplier Info > Submit Invoice (index 3)
- Backend: `services/Vendor_Submit_Invoice.Service.ss` (SS1.0)
