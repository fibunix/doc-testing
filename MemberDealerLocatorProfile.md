# Member Dealer Locator Profile — User Manual

## Overview

The Dealer Locator Profile extension allows members to update their business information that appears in the public Dealer Locator directory. Members can edit their website, upload a logo, write a business description, and select product categories.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Members | Update their dealer profile (website, logo, description, categories) |
| ISG Team | Reviews and applies submitted profile changes |
| Developers | Form-based profile editor with file upload and multi-select categories |

## Usage Flows

### Updating Your Dealer Locator Profile

1. Navigate to Member Info > **Update Dealer Locator Profile**
2. The form loads with your current profile data (if any exists)
3. Edit one or more of the following fields:

| Field | Type | Details |
|---|---|---|
| Website Address | URL input | Format: `http://www.example.com` |
| Logo | File upload | Accepts JPEG, PNG, GIF; max 5 MB; shows current logo thumbnail |
| Long Description | Textarea | Max 1,000 characters; detailed business description |
| Product Categories | Checkboxes | Select all categories that apply to your business |
| Dealer | Read-only text | Your dealer/member name (cannot be changed) |

4. Click **Submit** to send your changes for review
5. Success: green message "Profile updated successfully!" (auto-fades after 2 seconds)
6. Form automatically refreshes with the saved data

### Validation Errors

If any field is invalid, a red error message appears:
- "Please enter a valid website URL"
- "Please upload a valid image file (JPEG, PNG, or GIF)"
- "Logo file size must be less than 5MB"
- "Description must be less than 1000 characters"
- "Error updating profile. Please try again." (on save failure)

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Product categories | Backend configuration | Dynamic list of selectable categories | Fetched from NetSuite |

## Known Limitations & Edge Cases

- Logo must be an image file (JPEG, PNG, or GIF) — other formats are rejected
- Logo file size limit is **5 MB**
- Description has a **1,000-character** maximum
- Changes are submitted for review — they may not appear immediately in the Dealer Locator
- Only members can access this page — vendors are excluded
- Login is required

> Verify with stakeholder: Whether profile changes are applied immediately or require manual review by ISG staff.

## Developer Notes

- Route: `/dealer-locator-profile`
- Member-only: checks `isVendor === false`
- Menu entry under Member Info section
- Logo is uploaded as base64-encoded data
- Saves to NetSuite custom record fields
- Breadcrumb: Member Info > Update Dealer Locator Profile
