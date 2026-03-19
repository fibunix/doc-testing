# Member Submit PO for EDI — User Manual

## Overview

The Submit PO for EDI extension allows members to upload purchase order files in Excel format for EDI (Electronic Data Interchange) processing. Members can upload multiple files at once, filter submitted files by date, download previously submitted files, and access PO templates and documentation.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Members | Upload PO Excel files, browse/download submitted files, access templates |
| Store Admins | Configure template and documentation download URLs |
| Developers | File upload extension with multi-file support, date filtering, and progress tracking |

## Usage Flows

### Uploading PO Files

1. Navigate to "Submit PO for EDI" in the Member Info menu
2. Expand the **Submit PO** accordion section
3. Click **Choose Files** — the upload modal opens
4. Click the file input to select one or more Excel files (.xlsx, .xls)
5. Selected files appear in a list showing filename, size (KB), and a remove button
6. Optionally add a description in the text area
7. Click **Upload PO Files**
8. Progress message shows "Uploading X files..."
9. On success: "All files uploaded successfully (X/Y)" — modal closes after 2 seconds
10. On partial failure: lists which files failed with error reasons
11. File list refreshes automatically

**Upload Cancellation:** During upload, click **Cancel Upload** to stop. Files remain selected for retry.

### Downloading the PO Template

1. Expand the **Purchase Order Template** accordion section
2. Click **PO Template** to download the Excel template file
3. Click **Portal Documentation** to download usage documentation

### Filtering Files by Date

1. In the file list section, use the **Date Received** date picker
2. Select a date to filter files created on that date
3. Click **Clear** to remove the date filter and show all files

### Downloading a Submitted File

1. In the file list, locate the file you want
2. Click the **Download** button to save it to your computer

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| PO Template URL | `memberSubmitPOEDI.poTemplateUrl` | Download URL for the PO template file | Configured in NetSuite |
| Portal Documentation URL | `memberSubmitPOEDI.portalDocumentationUrl` | Download URL for documentation | Configured in NetSuite |
| Records per page | List configuration | Number of files shown per page | 50 |

## Known Limitations & Edge Cases

- Only **Excel files** (.xlsx, .xls) are accepted — other formats are rejected with an error
- Maximum file size is **10 MB** per file
- Duplicate files (same name and size) are silently ignored during selection
- Multiple files can be uploaded in a single batch
- If some files fail during batch upload, successful files are still saved — only failures are reported
- Sort options: by File Name (default) or by Date
- Only members can access this page — vendors are excluded
- Login is required

## Developer Notes

- Route: `/submit-po-edi`
- Member-only: checks `profile.isVendor === false`
- Files are converted to base64 before transmission to backend
- Upload uses FormData with progress tracking via XMLHttpRequest
- MIME type validation: `application/vnd.ms-excel`, `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`
- Backend stores files in NetSuite file cabinet
