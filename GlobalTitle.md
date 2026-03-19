# Global Title — User Manual

## Overview

The Global Title extension enhances the portal header and breadcrumb navigation. It displays the member's ISG member number at the top of pages and provides improved breadcrumb trails for navigation context.

## Who This Affects

| Audience | How They Interact |
|---|---|
| All Logged-in Users | See their member number displayed and enhanced breadcrumb navigation |
| Store Admins | CMS banner areas available above and below breadcrumbs |
| Developers | Global UI enhancement with no standalone route |

## Usage Flows

### Automatic Display

This extension works automatically on all pages:
- **Member Number**: Displays "Member #: [number]" at the top of the page (pulled from `custentity_bsp_crm_cust_id` profile field)
- **Breadcrumbs**: Shows the navigation path with clickable links (last item is active/non-linked)
- **Page Title**: Current page name shown as heading
- **CMS Banners**: Admin-managed content areas appear above and below the breadcrumb trail

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Member number field | `custentity_bsp_crm_cust_id` on customer record | The ISG member number displayed | From profile |
| CMS banner areas | NetSuite CMS | Content areas above/below breadcrumbs | Empty |

## Known Limitations & Edge Cases

- Member number only displays if the `custentity_bsp_crm_cust_id` custom field has a value
- Appears on both Shopping and My Account pages
- No standalone route — this is a global page enhancement

## Developer Notes

- No route registered — enhances existing page layout globally
- Targets both Shopping and MyAccount applications
- Reads `custentity_bsp_crm_cust_id` from the user profile custom fields
- CMS areas use path-filtered data attributes for content targeting
