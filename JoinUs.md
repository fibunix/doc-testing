# Join Us — User Manual

## Overview

The Join Us extension provides a public-facing membership inquiry form for businesses interested in joining ISG. Visitors fill out a comprehensive application with contact and business details, which is submitted to ISG for review.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Prospective Members (public) | Fill out and submit the membership inquiry form |
| ISG Staff | Receive and review submitted applications |
| Developers | Multi-section form with dynamic field options fetched from backend |

## Usage Flows

### Submitting a Membership Inquiry

1. Navigate to the **Join Us** page (`/join-us`) — no login required
2. Fill out the form sections:

**Contact Information:**
| Field | Type | Required |
|---|---|---|
| Company Name | Text | Yes |
| First Name | Text | Yes |
| Last Name | Text | Yes |
| Address | Text | Yes |
| City | Text | Yes |
| State | Dropdown (US states) | Yes |
| Zip Code | Text | Yes |
| Phone Number | 3-part input (area code + 3 digits + 4 digits) | Yes |
| Email | Email | Yes |
| Website | URL | No |

**Business Information:**
| Field | Type |
|---|---|
| Main Business Focus | Checkboxes (multiple selection) |
| Total Approximate Revenue | Dropdown |
| Account with Essendant/S.P. Richards? | Textarea |
| Buying group member? | Checkbox |
| Which buying group? | Text (conditional) |
| Sell on Amazon 3rd Party? | Checkbox |
| Amazon reseller name | Text (conditional) |
| Ship locally/nationwide/both? | Checkboxes |
| Total employees | Text |
| Sell brands/products in office products? | Checkbox |
| Warehouse products? | Checkbox |
| Operate own shopping cart? | Checkbox |
| How long in business? | Text |
| Main interest | Checkboxes (multiple selection) |
| Comments | Textarea |

3. Click **Submit**
4. On success: green message "Thank you. Your submission has been received." — form resets
5. On error: red alert box with specific error messages

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| State list | Site configuration | US states for dropdown | Auto-populated |
| Revenue options | Backend | Revenue range options for dropdown | Fetched from NetSuite |
| Business focus options | Backend | Categories for main business focus | Fetched from NetSuite |
| Interest options | Backend | Options for main interest checkboxes | Fetched from NetSuite |

## Known Limitations & Edge Cases

- **No login required** — this is a public-facing form on the shopping site
- Form options (revenue ranges, business focus, interests) are loaded dynamically from the backend
- Form resets completely after successful submission
- All required fields must be filled before submission is allowed
- Phone number requires all three parts (area code + first 3 + last 4)

## Developer Notes

- Route: `/join-us`
- Public page on the shopping application — no login or vendor/member gate
- Backend creates a record in NetSuite with the submitted data
- Dynamic field options fetched from NetSuite custom records or lists
- State dropdown populated from site configuration settings
