# CCT Events & Events List — User Manual

## Overview

The Events extensions display ISG event information on the portal. Events appear as cards on content pages (via a list widget) and as full detail pages when clicked. Content is managed through NetSuite custom records.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Portal Users | Browse upcoming events, view event details, navigate via links |
| Store Admins | Create and manage event records in NetSuite (`customrecord_cct_events`), configure list widget size |
| Developers | Two paired extensions: `CCT_Events` (detail view + routes) and `CCT_EventsList` (list widget) |

## Usage Flows

### Browsing Events from the List Widget

1. User sees the "ISG Events" widget on a content page (shopping or My Account)
2. Widget displays up to 5 events (configurable) with logo thumbnail, title, description, and date range
3. Click an event title or "Learn More" to open the full event detail page
4. Click "View All" to navigate to the full events page (`#events`)

### Viewing Event Details

1. User arrives at `#events/{slug}` (from list widget or direct link)
2. Page displays full event information including rich HTML content
3. Breadcrumb navigation shows: Events > [Event Title]
4. CMS areas allow additional content placement around the event details

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| List size | `custrecord_cct_events_list_size` on list config record | Number of events shown in widget | 5 |
| Event title | `custrecord_cct_events_title` | Event name displayed as heading | — |
| Event logo | `custrecord_cct_events_logo` | Image URL shown as thumbnail in list, full size on detail | — |
| Description | `custrecord_cct_events_description` | Short text shown in list cards | — |
| Start/End date | `custrecord_cct_events_start_date` / `_end_date` | Displayed as formatted date range (e.g., "March 1–5, 2024") | — |
| Slug | `custrecord_cct_events_slug` | URL-friendly identifier for detail page routing | — |
| Details HTML | `custrecord_cct_events_details` | Rich text content shown on detail page | — |

## Known Limitations & Edge Cases

- Events list has no client-side pagination, search, or filtering — it shows a fixed number of items
- Only **active** events are displayed (inactive records are filtered out server-side)
- Events are sorted by internal ID descending (newest first) — there is no date-based sort
- Logo images in the list widget are resized to thumbnail format automatically
- No login is required to view events (public-facing on shopping app)

## Developer Notes

- **CCT_Events** registers routes `#events/:slug` and handles detail pages via `ISG.CCT_EventsDetail.View.js`
- **CCT_EventsList** is a CMS widget (Custom Content Type) with no routes — placed via NetSuite CMS
- Both extensions target Shopping and MyAccount apps
- Backend uses SS1.0 ServiceController pattern
- NetSuite record: `customrecord_cct_events`
- Service endpoints: `ISG.CCT_EventsDetail.Service.ss`, `ISG.CCT_EventsList.Service.ss`
