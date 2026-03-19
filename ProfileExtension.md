# Profile Extension — User Manual

## Overview

The Profile Extension identifies whether a logged-in user is a vendor or a member by checking a custom field on their NetSuite profile. This determination controls which portal features and menus are visible throughout the entire application.

## Who This Affects

| Audience | How They Interact |
|---|---|
| All Logged-in Users | Automatically classified as vendor or member at login |
| Store Admins | Set the `custentity_bsp_related_vendor` field on customer/contact records in NetSuite to designate vendors |
| Developers | Wraps `Profile.Model.get()` server-side to inject `isVendor` and `vendor` properties |

## Usage Flows

### Automatic Vendor/Member Detection

1. User logs in with their email and password (standard SuiteCommerce login)
2. The system loads the user's profile including all custom fields
3. If `custentity_bsp_related_vendor` has a value: user is classified as a **vendor**
4. If the field is empty: user is classified as a **member**
5. All portal extensions check this classification to show/hide features accordingly

**Vendor users see:** File Processing, Submit Invoice, Rebate Templates, Quarterly Cost List, Tax Certificates, Portal Documentation

**Member users see:** Accounting Center, Invoices, Rebates, PO Reports, Supplier Directory, Dealer Locator Profile, and more

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Vendor association | `custentity_bsp_related_vendor` on customer/contact record | Links user to vendor record; presence = vendor | Empty (member) |

## Known Limitations & Edge Cases

- A user is either a vendor or a member — there is no dual-role support
- The field is checked on every profile retrieval, not just at login
- If the field is set but has no value (empty string), the user is treated as a member
- This extension runs across all three SCA applications: Shopping, My Account, and Checkout
- No UI is provided — this is entirely behind-the-scenes classification

## Developer Notes

- No route or menu entry — server-side profile enhancement only
- SSP Library: `Modules/ProfileExtension/SuiteScript/BSP.ProfileExtension.js`
- Uses `_.wrap()` on `Profile.Model.get()` to inject `isVendor` (boolean) and `vendor` (record ID) properties
- Frontend entry point (`JavaScript/BSP.ProfileExtension.js`) has an empty `mountToApp` — all logic is server-side
- Custom field: `custentity_bsp_related_vendor`
- Targets SCA, SCS >= 23.2
