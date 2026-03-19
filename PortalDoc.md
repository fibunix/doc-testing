# Portal Documentation — User Manual

## Overview

The Portal Documentation extension provides a dedicated page for vendor-facing help content and documentation. The page content is managed through the NetSuite CMS, allowing administrators to update documentation without code changes.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Vendors | Access help documentation and guides for using the portal |
| Store Admins | Manage page content via CMS areas in NetSuite |
| Developers | Simple CMS-driven content page with no dynamic data |

## Usage Flows

### Viewing Portal Documentation

1. Navigate to **Portal Documentation** in the My Account menu
2. The page displays CMS-managed content (guides, instructions, FAQs, etc.)
3. Content is divided into a main area and a footer area, both managed via CMS

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Main content | NetSuite CMS (path-filtered) | Primary documentation content area | CMS-managed |
| Footer content | NetSuite CMS (path-filtered) | Footer documentation content area | CMS-managed |

## Known Limitations & Edge Cases

- Only vendors can access this page — members are excluded
- Login is required
- Page content is entirely CMS-driven — no dynamic data from backend services
- Content updates require CMS editing in NetSuite, not code changes

## Developer Notes

- Route: `/portal-documentation`
- Vendor-only: checks `isVendor` flag
- Menu entry at index 10 (near bottom of My Account menu)
- Two CMS data areas with path-filtered content
- No backend service calls — purely static content page
