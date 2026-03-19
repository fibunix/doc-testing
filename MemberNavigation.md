# Member Navigation — User Manual

## Overview

The Member Navigation extension provides the complete menu structure and content pages for the member portal. It defines the sidebar navigation with five main sections (Member Center, Accounting Center, File Processing, Programs, and Member Info) and includes several static content pages such as the Member Center home, Accounting Help, File Instructions, and Policies & Procedures.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Members | Navigate the portal via sidebar menu, access help pages and documentation |
| Store Admins | Configure menu items, carousel images, and downloadable document URLs |
| Developers | Central navigation extension that structures the entire member portal experience |

## Usage Flows

### Navigating the Portal

The left sidebar menu provides access to all portal features:

**1. Member Center** (Home)
- Image carousels with ISG content
- News and Events sections (CMS-managed)
- Quick links to Accounting Help and file downloads

**2. Accounting Center**
- Accounting Home (dashboard)
- Invoices
- Statements
- Debit Memo Request
- Banking Setup
- Accounting Center Help (FAQ accordion)

**3. File Processing**
- Price Files & OPUS Instructions (10 collapsible sections)

**4. Programs** (9+ categories)
- Cost Comparator Tool, EPIC Business Essentials, Furniture
- INTEC and INTEC Supplier Programs, ISG PLUS
- Jan San (Facility Supplies, Supplier Directory)
- Marketing (5 sub-items), Pinnacle (5 sub-items)

**5. Member Info**
- Change Password, Address Book, Profile Information
- Rebates, Purchase Summary Report (PSR)
- Update Dealer Locator Profile, User Setup
- Submit PO for EDI
- Policies, Procedures & ByLaws (with sub-pages)

### Viewing Accounting Center Help

1. Navigate to Accounting Center > Accounting Center Help
2. Page shows 7 collapsible accordion panels:
   - Invoice Pickup, Make Payment, Quick Pay, Invoices, Statements, Create Debit Memo Requests, Banking Setup
3. Click any panel header to expand and read the help content

### Viewing Price Files & OPUS Instructions

1. Navigate to File Processing > Price Files & OPUS Instructions
2. Page shows 10 collapsible accordion panels covering:
   - Flyer/Direct Buy/ECP Price Files, SPR/ACD and BSN files, DDMS OPUS Instructions, Freight Changes, New Products

### Viewing Policies, Procedures & ByLaws

1. Navigate to Member Info > Policies, Procedures & ByLaws
2. Main page has 11 collapsible sections covering membership, ordering, invoicing, payment, freight, termination, and patronage policies
3. Sub-pages available:
   - Policies and Procedures (detailed document with download link)
   - Code of Ethics (3 main sections: Introduction, Business Conduct Guidelines, Administration)
   - ISG ByLaws (with PDF download link)

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Menu items | `MyAccountMenu.json` configuration | All menu entries, URLs, and hierarchy | Pre-configured |
| Carousel images | Extension configuration | Images for Member Center carousels | Configured in NetSuite |
| Download URLs | CMS areas / configuration | URLs for template and documentation downloads | Configured per document |

## Known Limitations & Edge Cases

- Only members see this navigation — vendors have a different menu structure
- Menu uses accordion behavior: expanding one parent section collapses others
- Menu state persistence: parent menus stay open when clicking sub-items within them
- Responsive behavior: sidebar adapts to phone, tablet, and desktop layouts
- Mobile sidebar closes automatically when switching between mobile and desktop viewports
- Content pages (help, instructions, policies) use collapsible accordions — only one section open at a time

## Developer Notes

- Routes: `/member-center`, `/accounting-help`, `/file-instructions`, `/policies-procedures-bylaws` (with sub-routes for policies, code of ethics, bylaws)
- Member-only: checks `isVendor` flag in user profile
- Targets both Shopping (header nav) and MyAccount (sidebar) applications
- Templates contain static HTML content for help pages, policies, and procedures
- CMS areas integrated for dynamic content placement on Member Center page
- Menu registration uses `MyAccountMenu` component with index-based ordering
