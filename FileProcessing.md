# File Processing — User Manual

## Overview

The File Processing extension allows vendors to upload, download, edit, and comment on various business files (pricing, promotions, rebates, content). It provides a full file management interface with upload modal, edit capabilities, and per-file commenting.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Vendors | Upload, download, edit, and comment on files |
| Store Admins | Configure file types, size limits, and retention settings |
| Developers | Full CRUD file management extension with modal-based forms |

## Usage Flows

### Viewing Your Files

1. Navigate to the **File Processing** menu and select a file category:
   - Tax Certificates
   - Website Pricing/Promotion/Content Files
   - Quarterly Cost-List Processing Files
2. The page displays a table with columns: File name, Status, Date uploaded, File type
3. Sort files by filename using the column header
4. Use pagination controls to browse through files (default 50 per page)

**Empty state:** "You don't have any Files at the moment, try adding one now!"

### Uploading a New File

1. Click the **Add File** button
2. In the upload modal:
   - Click to select a file (accepted formats: .csv, .xlsx, .xls, .txt, .pdf, .doc, .docx)
   - Select a **File Type** from the dropdown:
     - Pricing file
     - Promotion and Announcements
     - Pinnacle Pricing File
     - Pinnacle Promotion and Announcements
     - Rebate file
     - Content file
   - Optionally add a **Description**
3. Click **Upload** — a progress indicator shows upload status
4. On success, the modal closes and the file list refreshes

### Editing a File

1. Click the **Edit** button on any file row
2. The edit modal shows:
   - Current file name and status (read-only)
   - Editable file name field
   - Option to replace the file with a new upload
   - File type dropdown
   - Description field
3. Make changes and click **Save**
4. Success/error message appears

### Adding a Comment to a File

1. Click the **Add Comment** button on any file row
2. Enter your comment in the text area
3. Click **Submit** to save the comment

### Downloading a File

1. Click the **Download** button on any file row
2. The file downloads to your computer

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Max file size | Extension configuration | Maximum upload file size in MB | 10 |
| Allowed file types | Extension configuration | Accepted file extensions | csv, xlsx, xls, txt, pdf, doc, docx |
| Default status | Extension configuration | Status assigned to newly uploaded files | pending |
| Auto-process | Extension configuration | Whether files are processed automatically on upload | false |
| Retention days | Extension configuration | How long files are retained | 90 |

## Known Limitations & Edge Cases

- Maximum file size is **10 MB**
- Only accepted file formats can be uploaded — other types are rejected
- File status cannot be changed by the user (admin-only field)
- Only vendors can access this extension — members are excluded
- Login is required

## Developer Notes

- Route: `/website-files`
- Vendor-only: checks `profile.isVendor === true`
- Menu entry under "File Processing" group with sub-entries for Tax Certificates, Website files, and Quarterly Cost files
- Backend uses SS1.0 ServiceController pattern
- Files stored in NetSuite file cabinet
- Upload uses FormData with progress tracking
