# Member List — User Manual

## Overview

The Member List extension displays a downloadable member list file on the member's dashboard. It provides a simple widget showing the current member list file with its name, creation date, size, and a download button.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Members | Download the current member list file |
| Store Admins | Place the member list file in the configured NetSuite folder (default folder ID: 5873) |
| Developers | Dashboard widget with file metadata display and download action |

## Usage Flows

### Downloading the Member List

1. On the dashboard/overview page, locate the "Member List" widget
2. The widget shows:
   - Filename of the current member list
   - Date the file was created (MM/DD/YYYY HH:MM:SS)
   - File size (auto-formatted as Bytes, KB, MB, or GB)
3. Click the **Download** button to save the file to your computer
4. Click the **Refresh** button to check for a newer version

### When No File Is Available

- If no member list file exists, the widget displays: "No member list found" with a warning icon
- If loading fails, an error message appears: "Failed to load member list information" with a **Try Again** button

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Folder ID | `memberlist.folderId` in extension configuration | NetSuite file cabinet folder containing the member list | 5873 |

## Known Limitations & Edge Cases

- Only one file is displayed (the current member list from the configured folder)
- No search, pagination, or filtering — this is a single-file widget
- Only members can see this widget — vendors are excluded
- Login is required
- Shows a loading spinner with "Loading..." text while fetching file information

## Developer Notes

- No standalone route — this is a dashboard widget displayed in the "Overview" section
- Member-only: checks `profile.isVendor === false`
- Uses SuiteScript 2.x backend service for file operations
- Fetches file metadata from the configured NetSuite file cabinet folder
