# Suppliers Directory — User Manual

## Overview

The Suppliers Directory is a comprehensive, searchable catalog of ISG suppliers available to members. Members can search by name, category, brand, and various program attributes, then view detailed supplier profiles including program terms, rebate information, marketing terms, contact details, and downloadable files.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Members | Search suppliers, view detailed profiles, download pricing and promotion files |
| Store Admins | Manage supplier records, programs, categories, and brands in NetSuite |
| Developers | Two-view extension: paginated directory list + detailed supplier profile page |

## Usage Flows

### Searching the Supplier Directory

1. Navigate to **Supplier Directory** in the My Account menu
2. Use any combination of search filters:

| Filter | Type | Description |
|---|---|---|
| Alphabet | Dropdown | Filter suppliers by first letter (A–Z) |
| Category | Autocomplete | Search by product category |
| Keyword | Text input | Free-text search by supplier name |
| Supplier Type | Dropdown | Filter by supplier classification |
| Brand | Dropdown | Filter by brand name |
| Preferred Supplier | Dropdown | Yes / No / Pinnacle Only |
| Use or Lose | Dropdown | Yes / No |
| Local CoOp | Dropdown | Yes / No |
| EDI | Dropdown | Yes / No |

3. Click to search — results display as a card grid with supplier logo, name, and program info
4. Use pagination to browse through results
5. Click **Clear Filters** to reset all search criteria

**Empty state:** "There are no suppliers yet!"

### Viewing Supplier Details

1. Click a supplier name or card to open the detail page (`/supplierdetails/:id`)
2. The detail page shows:

**Header:**
- Supplier logo, company name, phone, website, EDI certification status

**Members & Shipment Terms:**
- Standard Terms, Member Terms (highlighted), Minimum Order, Prepaid Freight
- Lead Time, Dealer P/U Allowance, Carrier options, FOB Centers, Drop Ship availability

**Optimum Program Value:**
- Program value percentage

**Rebate Information:**
- Direct Rebates: Volume, Growth, Category-specific
- Product/Category Rebates with per-product details
- Wholesale Rebates (if applicable)
- Payment methods for each rebate type

**Marketing Terms:**
- Catalog Allowance, HQ Marketing Allowance, Local Co-op, Use or Lose indicator

**Comments:**
- Supplier-specific notes and comments (rich HTML content)

**Product Categories & Brands:**
- Full list of categories and brand names the supplier offers

**Files & Promotions:**
- Pricing Files (downloadable)
- Pinnacle Pricing Files (marked with Pinnacle logo, if applicable)
- Promotions & Announcements (downloadable)

**Contact Information:**
- Customer Service: name, phone, cell, fax, email
- Bid Coordinator: name, phone, fax, email

### Switching Program Years

1. On a supplier detail page, look for program year navigation
2. Click **View Last Year's Program** or **View Current Program** to switch
3. Other available program years appear as buttons

### Downloading Supplier Files

1. On the supplier detail page, scroll to the Files & Promotions section
2. Click any pricing file or promotion link to download

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Supplier records | NetSuite custom records | Supplier data including terms, rebates, contacts | Managed in NetSuite |
| Programs | `CUSTOMRECORD_BSP_PROGRAM` | Program year and terms data | Managed in NetSuite |
| Brands | `CUSTOMRECORD_BSP_BRANDS` | Brand records linked to suppliers | Managed in NetSuite |
| Categories | `CUSTOMRECORD_BSP_CATEGORIES` | Product category records | Managed in NetSuite |

## Known Limitations & Edge Cases

- Only **members** can access this directory — vendors are excluded
- Only one sort option available: **Sort By Name**
- Filters persist in the URL — use browser back/forward to navigate filter history
- Supplier Type and Brand dropdowns start disabled/empty until data loads
- Program year switching loads different terms and rebate data for the same supplier
- Pagination resets to page 1 when any filter changes
- Some suppliers may not have all sections populated (contacts, files, rebates)

## Developer Notes

- Routes: `/suppliersdirectory`, `/supplierdetails/:id`
- Member-only: checks `isVendor === false`
- Menu entry: "Supplier Directory"
- NetSuite custom records: `CUSTOMRECORD_BSP_PROGRAM`, `CUSTOMRECORD_BSP_BRANDS`, `CUSTOMRECORD_BSP_CATEGORIES`
- Backend searches supplier records with multi-field filtering
- Program data is year-based with switchable views
- File downloads link to NetSuite file cabinet documents
