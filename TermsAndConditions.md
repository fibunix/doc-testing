# Terms and Conditions — User Manual

## Overview

The Terms and Conditions extension enforces periodic acceptance of the portal's terms and conditions. When a user's acceptance has expired (based on a configurable validity period), they are automatically redirected to the terms page and must accept before continuing to use the portal.

## Who This Affects

| Audience | How They Interact |
|---|---|
| All Logged-in Users | Must accept terms when they expire; redirected automatically |
| Store Admins | Configure validity period, enable/disable feature, manage terms content via CMS |
| Developers | Auto-redirect extension with profile field tracking and CMS content |

## Usage Flows

### Accepting Terms and Conditions

1. After logging in, the system checks when you last accepted the terms
2. If your acceptance has expired (default: 30 days), you are automatically redirected to the Terms and Conditions page after a 1-second delay
3. The page displays the current terms (CMS-managed content)
4. Click **Accept Terms and Conditions** to accept
5. Your acceptance date is saved to your profile
6. You are redirected to the home page (`/`)

### Re-acceptance

This flow repeats automatically each time the validity period expires. There is no manual way to view or re-accept terms outside the automatic redirect cycle.

## Configuration & Settings

| Setting | Location | Description | Default |
|---|---|---|---|
| Enabled | Extension configuration | Turn the terms enforcement on or off | Enabled |
| Validity days | Extension configuration | How many days before users must re-accept | 30 |
| Page URL | Extension configuration | URL path for the terms page | `/terms-and-conditions` |
| Terms content | NetSuite CMS (path-filtered) | The actual terms and conditions text | CMS-managed |
| Acceptance date | `custentity_bsp_accepted_terms_date` on user profile | Timestamp of last acceptance | Set on accept |

## Known Limitations & Edge Cases

- The feature can be **completely disabled** via configuration
- Users who are not logged in will not see or be redirected to the terms page
- Redirect happens 1 second after page load (slight delay to avoid conflicts with other page loads)
- If the `custentity_bsp_accepted_terms_date` field has never been set, the user is treated as never having accepted
- The acceptance date comparison is based on calendar days from the stored date
- Terms content is entirely CMS-managed — changing terms requires CMS editing in NetSuite
- Both vendors and members are subject to terms acceptance

## Developer Notes

- Route: configurable, default `/terms-and-conditions`
- Targets both Shopping and MyAccount applications
- Checks `custentity_bsp_accepted_terms_date` profile field against current date minus validity days
- Redirect uses `setTimeout` with 1-second delay in `mountToApp`
- Acceptance saves current date to `custentity_bsp_accepted_terms_date` via profile update
- CMS content area uses path-filtered data attribute for content targeting
