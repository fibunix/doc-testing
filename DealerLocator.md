# Dealer Locator — User Manual

## Overview

The Dealer Locator is a public-facing search tool that helps visitors find ISG-affiliated dealers by location, product category, or name. It displays dealers in a card grid with contact details and links to detailed dealer profile pages.

## Who This Affects

| Audience | How They Interact |
|---|---|
| All Visitors (no login required) | Search for dealers by location, name, or product category |
| Members | Their profile data appears in search results (managed via Dealer Locator Profile extension) |
| Store Admins | Configure mile radius options, other locations, and zip code data file |

## Usage Flows

### Searching for Dealers

1. Navigate to the **Dealer Locator** page (`/dealerlocator`)
2. Use one or more search filters:

**By Location:**
| Filter | Type | Description |
|---|---|---|
| Zip Code | Text input | Enter a zip code to search nearby |
| Within Miles | Dropdown | Radius: 5, 10, 20, 30, 50, 100, 150, or 200 miles |
| City | Text input | Enter a city name |
| State | Dropdown | Select from all US states |

**By Other Location:**
| Filter | Type | Description |
|---|---|---|
| Location | Dropdown | Non-US locations (e.g., Aruba, Cayman Islands, Virgin Islands) |

**Additional Filters:**
| Filter | Type | Description |
|---|---|---|
| Dealer Name | Text input | Search by dealer/company name |
| Dealers that offer | Dropdown | Product categories (Office Supplies, Furniture, Technology, etc.) |

3. Click **Locate Dealer** to search, or **Clear Filters** to reset all fields
4. Results appear as a grid of 3 dealer cards per row (responsive on mobile)

### Search Results

Each dealer card shows:
- **Dealer Name** (heading)
- **ISG Member ID** badge (e.g., "ISG #12345") if available
- **Address** (with map icon)
- **Contact Name** (with person icon, if available)
- **Phone** (clickable tel: link)
- **Fax** (if available)
- **Email** (clickable mailto: link)
- **Website** (clickable, opens in new tab)
- **View** arrow link to full details page

Pagination controls appear above and below results showing current page, total pages, and total results.

**No results:** "No dealers found! Try adjusting your search criteria or clearing filters."

### Viewing Dealer Details

1. Click **View** on any dealer card
2. The detail page (`/dealerdetails/:id`) shows:
   - Dealer logo (or placeholder with company name)
   - ISG member badge
   - Full address, contact person, phone, fax, email, website
   - **Product Categories** — tags listing all categories the dealer offers
   - **About** section — business description
3. Breadcrumb: Dealer Locator > [Dealer Name]

### Sharing Search Results

All filter selections are preserved in the URL as query parameters. Copy the URL to share a specific search with others:
```
/dealerlocator?search=office&state=IL&miles=20&page=1
```

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Miles options | `DealerLocator.json` | Dropdown values for radius search | 5, 10, 20, 30, 50, 100, 150, 200 |
| Other locations | `DealerLocator.json` | Non-US location dropdown values | Aruba, Cayman Islands, Virgin Islands |
| Zip code file ID | `DealerLocator.json` | NetSuite file ID for zip code distance data | 77514 |
| Product categories | Backend | Dynamic list of dealer categories | Fetched from NetSuite |

## Known Limitations & Edge Cases

- **No login required** — this is a public-facing page on the shopping site
- Only one sort option available: Sort By Name (ascending/descending)
- Search updates trigger on field blur (leaving a text field) or dropdown change
- Changing any filter resets pagination to page 1
- Filters persist in the URL and survive browser back/forward navigation
- Responsive layout: 3 cards per row on desktop, 1 on mobile
- Dealer detail "About" section uses a default ISG description if the dealer hasn't provided a custom one

## Developer Notes

- Routes: `/dealerlocator`, `/dealerlocator?*params`, `/dealerdetails/:id`
- No login gate — available to all users on the shopping app
- Uses `focusout` events on text inputs and `change` events on dropdowns for real-time filtering
- URL query parameters: `search`, `zipcode`, `state`, `city`, `miles`, `category`, `otherLocation`, `page`, `sort`, `order`
- Backend searches NetSuite dealer records with location-based filtering
- Zip code distance calculation uses a CSV data file stored in NetSuite file cabinet
- Categories are fetched dynamically from NetSuite custom records
