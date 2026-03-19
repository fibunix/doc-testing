# Payment Instrument Account — User Manual

## Overview

The Payment Instrument Account extension enhances the ACH (Automated Clearing House) bank account payment setup within the portal. It modifies the bank account number display and handling in the existing payment instrument forms.

## Who This Affects

| Audience | How They Interact |
|---|---|
| Members & Vendors | See improved bank account number handling in payment setup |
| Store Admins | No additional configuration needed |
| Developers | Extends existing payment instrument form behavior |

## Usage Flows

### Automatic Enhancement

This extension works automatically when users interact with ACH/bank account payment setup:
- Displays bank account number from profile data if available
- Enhances the bank account number field display and handling
- Integrates with the existing payment setup workflow

## Configuration & Settings

No additional configuration is required — this extension enhances existing payment form behavior.

## Known Limitations & Edge Cases

- Only affects ACH/bank account payment forms — credit card forms are not modified
- Available to both vendors and members
- Login is required
- No standalone route or menu entry — this is a form enhancement

## Developer Notes

- No standalone route — enhances existing payment instrument forms
- Targets the MyAccount application
- Extends the ACH payment instrument view/model behavior
- Reads bank account data from user profile
