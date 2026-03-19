# User Setup — User Manual

## Overview

The User Setup extension allows company administrators (principal users) to manage portal access for their contacts. Administrators can add new users, edit their details, assign role-based privileges, and grant or revoke portal access.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Company Administrators | Add/edit/remove contacts, assign privileges |
| Contacts | Receive portal access and role-based permissions |
| Developers | Contact CRUD with hierarchical privilege system backed by NetSuite custom records |

## Usage Flows

### Viewing Contacts

1. Navigate to Settings > **User Setup** in the My Account menu
2. The page displays a list of all contacts for your company showing: name, email, role, and access status

### Adding a New Contact

1. Click **Add Contact**
2. Fill in the modal form:
   - First Name (required)
   - Last Name (required)
   - Email (required)
   - If granting portal access: set Password and Confirm Password
   - Toggle **Give Access** checkbox to grant portal login
3. Click **Save** — the new contact appears in the list

### Editing a Contact

1. Click the **Edit** button on a contact row
2. Modify fields: First Name, Last Name, Email, Phone
3. Click **Save** — changes are applied immediately

### Managing Privileges

1. Click the **Privileges** button on a contact row
2. The privileges modal shows checkboxes organized by role:

**Principal User** — checking this enables ALL privileges and disables individual controls

**User Types:**
| User Type | Included Privileges |
|---|---|
| Accounting | Banking Setup, Debit Memo Request, Invoice Pickup, Make Payment, Message Board, Remainder of Site |
| Purchasing | Invoice Pickup, Message Board, Rebate Access, Purchasing Summary Report |
| General | Remainder of Site, Supplier Directory |

3. Check a User Type to enable all its privileges at once
4. Or check individual privileges manually
5. Click **Save** to apply the privilege changes

### Granting or Revoking Portal Access

1. Click the **Remove Access** button on a contact row
2. A confirmation dialog appears
3. Confirm to toggle the contact's access status (grant ↔ revoke)
4. The list refreshes to show the updated status

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Privilege record | `customrecord_bsp_user_privileges` in NetSuite | Stores per-contact privilege flags | Created per contact |

## Known Limitations & Edge Cases

- Password is only required when **first granting access** — editing a contact does not require re-entering the password
- **Principal User** overrides all individual settings — when checked, all other checkboxes are automatically enabled and locked
- Some privileges appear in multiple user types (e.g., "Invoice Pickup" is in both Accounting and Purchasing) — checking either user type enables the shared privilege
- Deleting a contact removes them from both the contact list and their NetSuite contact record
- Available to both vendors and members with administrator access
- Login is required

## Developer Notes

- Route: `/user-setup`
- Menu: Settings > User Setup (index 4)
- Backend: SuiteScript 2.x (`SuiteScript2/Contact.Model.js`, `SuiteScript2/UserSetup.Service.ss`)
- NetSuite records: Contact (standard), Customer contactroles sublist, `customrecord_bsp_user_privileges` (custom)
- Privilege field mapping: `custrecord_bsp_priv_*` fields on the custom record
- Contact operations modify both the Contact record and the Customer's contactroles sublist
