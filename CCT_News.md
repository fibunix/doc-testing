# CCT News & News List — User Manual

## Overview

The News extensions display ISG news articles on the portal. A list widget shows recent headlines, and clicking through opens a full article detail page. Content is managed through NetSuite custom records.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Portal Users | Browse recent news headlines, read full articles |
| Store Admins | Create and manage news records in NetSuite (`customrecord_cct_news`), configure list widget size |
| Developers | Two paired extensions: `CCT_News` (detail view + routes) and `CCT_NewsList` (list widget) |

## Usage Flows

### Browsing News from the List Widget

1. User sees the "Stay in the News!" widget on a content page
2. Widget displays up to 5 news items (configurable) with publication date, title, and description preview
3. Click a news title or "Read More" to open the full article
4. Click "View All" to navigate to the full news page (`#news`)

### Reading a News Article

1. User arrives at `#news/{slug}` (from list widget or direct link)
2. Page displays the full article as rich HTML content
3. Breadcrumb navigation shows: News > [Article Title]
4. CMS areas allow additional content placement around the article

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| List size | `custrecord_cct_news_list_size` on list config record | Number of news items shown in widget | 5 |
| Title | `custrecord_cct_news_title` | Article headline | — |
| Date | `custrecord_cct_news_date` | Publication date (displayed as MM/DD/YYYY) | — |
| Description | `custrecord_cct_news_description` | Preview text shown in list cards | — |
| Slug | `custrecord_cct_news_slug` | URL-friendly identifier for detail page routing | — |
| Details HTML | `custrecord_cct_news_details` | Rich text content shown on detail page | — |

## Known Limitations & Edge Cases

- News list has no client-side pagination, search, or filtering — it shows a fixed number of items
- Only **active** news items are displayed (inactive records filtered out server-side)
- News items sorted by internal ID descending (newest first) — no date-based sort
- News items have no images (unlike events which have logos)
- No login required to view news (public-facing on shopping app)

## Developer Notes

- **CCT_News** registers routes `#news/:slug` and handles detail pages via `ISG.CCT_NewsDetail.View.js`
- **CCT_NewsList** is a CMS widget (Custom Content Type) with no routes — placed via NetSuite CMS
- Both target Shopping and MyAccount apps
- Backend uses SS1.0 ServiceController pattern
- NetSuite record: `customrecord_cct_news`
- Service endpoints: `ISG.CCT_NewsDetail.Service.ss`, `ISG.CCT_NewsList.Service.ss`
