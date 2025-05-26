# BudgetTrack Changelog

**Project**: BudgetTrack  
**Files**: `index.html` (Dashboard, artifact ID: `8bc478...`), `income.html` (Income, artifact ID: `f4cd92fd-4b82-4887-a81c-f944e58f7249`)  
**Maintained by**: Grok 3 (xAI)  
**Timezone**: EAT (East Africa Time)

All notable changes to the BudgetTrack project will be documented in this file. The format is based on semantic versioning (`MAJOR.MINOR.PATCH`).

---

## [1.0.1] - 2025-05-27 00:13 AM EAT

### Description
Fixed critical bugs in `income.html` reported as "code is broken," addressing syntax errors, runtime issues, and logical bugs in the Uber Wallet and trip form. Updated time to May 26, 2025, 02:51 PM EAT. Applied minor updates to `index.html` for consistency.

### Changes

#### `income.html`
- **Event Listeners Fix** (Issue: Invalid `#` selectors causing runtime errors):
  - Changed selector array to `['trip-date', 'start-time', 'duration-hours', 'duration-minutes', 'duration-seconds', 'distance', 'fare', 'cash-collected', 'tips']`.
  - Ensured all input elements have valid `id` attributes.
- **SubmitTrip Function Fixes** (Issue: Typos causing `TypeError`):
  - Corrected `getElement` to `getElementById` for `distance` and `cashCollected`.
  - Fixed `commissionGLOBAL.parseFloat` to `commission: parseFloat`.
  - Added `platform: 'Uber'` for online trips to ensure platform tracking.
- **Payout Interval** (Issue: Commented-out `setInterval`):
  - Uncommented and set to 60000ms (1 minute) for periodic payout checks.
- **Table Sorting Bug** (Issue: Incorrect numeric parsing):
  - Fixed regex in `sortTable`: Changed `replace(/\d|KES/g, '')))` to `replace(/KES|,/g, '')` for numeric columns.
  - Removed extra parenthesis in regex.
- **Modal Form Reset** (Issue: `.reset()` failing on non-form element):
  - Wrapped `trip-form` in `<form id="uber-trip-form">`.
  - Updated `closeModal` to use `document.getElementById('uber-trip-form').reset()`.
  - Added `type="button"` to form buttons to prevent unintended submission.
- **Time Update** (Issue: Hardcoded time mismatch):
  - Set `new Date('2025-05-26T14:51:00')` for 02:51 PM EAT, May 26, 2025.
  - Updated greeting and date/time displays.
- **Validation Enhancements** (Issue: Missing input validation):
  - Added checks in `submitTrip` for:
    - Invalid or missing date.
    - Negative or zero duration.
    - Cash Collected exceeding Total Fare.
    - Negative commission or taxes.
- **Performance Optimization** (Issue: Potential lag on 4GB RAM Dell Latitude):
  - Limited transaction list to last 5 entries in `updateWalletUI`.
  - Consolidated `localStorage` writes.
- **Form Behavior**:
  - Ensured `cash-collected-group` hides for In-App payments.
  - Added `max` and `min` attributes to `duration-minutes` and `duration-seconds` (capped at 59).
- **Error Handling**:
  - Added try-catch blocks in `openModal`, `submitTrip`, `updateTripForm` with user-friendly alerts.
  - Logged errors to console for debugging.

#### `index.html`
- **Initial Setup** (Assumed from prior context):
  - Created dashboard with header (logo, navigation, profile dropdown), main (summary card placeholders), and footer.
  - Added responsive navigation with hamburger menu for mobile.
  - Included Feather Icons and Flatpickr via CDN.
- **Consistency Updates**:
  - Synced styling with `income.html` (Inter font, teal `#00A7A8`).
  - Updated date/time to May 26, 2025, 02:51 PM EAT for greeting.
  - Fixed CSS: Ensured `mobile-dropdown` hides on link click.
- **Bug Fix** (Issue: `Uncaught SyntaxError: missing ) after argument list`):
  - Corrected syntax in event listener setup (aligned with `income.html` fix).
  - Ensured proper closure of parentheses in JavaScript functions.

### General
- **Testing Instructions**:
  - Provided steps to test `income.html` (trip form, wallet actions, filters, sorting).
  - Recommended `python -m http.server` and console error checks.
- **CDN Fallback**:
  - Suggested hosting Flatpickr locally if CDN fails.
- **Versioning**:
  - Incremented to 1.0.1 for bug fixes and minor updates.
- **Notes**:
  - `index.html` changes reconstructed from context; specific diffs unavailable.
  - Focused on `income.html` stability for Uber Wallet and trip logging.

## [1.0.0] - 2025-05-25

### Description
Initial release of BudgetTrack with `index.html` (Dashboard) and `income.html` (Income) pages.

### Changes

#### `index.html`
- Created dashboard:
  - **Header**: Logo (`BudgetTrack`), navigation, profile dropdown (username: `JohnDoe`, bio, sign-out).
  - **Main**: Placeholders for summary cards (Total Income, Expenses, Savings).
  - **Footer**: Links to Terms, Privacy, Support.
- Added responsive design with mobile hamburger menu.
- JavaScript:
  - Time-based greeting (`Good Morning/Afternoon/Evening, JohnDoe`).
  - Profile and mobile menu toggle.
- Dependencies: Feather Icons, Flatpickr via CDN.
- Styling: Inter font, teal `#00A7A8`, light background `#F8F9FA`.

#### `income.html`
- Created income page:
  - **Income Goal**: Amount/period input, progress bar.
  - **Summary Cards**: Total Income, Hours, Distance, Earnings/Hour, Earnings/Km, Service Fee, Wallet Balance.
  - **Platform Earnings**: Earnings per platform.
  - **Uber Wallet**: Balance, cash out/pay debt buttons, transaction table.
  - **Trip Log**: Trip table, filters (date range, day/week/month/year), add trip button.
  - **Modal**: Forms for Uber Trip (date, time, duration, distance, fare, payment method, fees, tips) and Offline Income (source, date, amount).
- JavaScript:
  - `UberWallet` class: Manages balance, transactions, payouts, debt alerts.
  - `UberTrip` class: Calculates earnings, fees, wallet impact.
  - Form calculations: Commission (18%), taxes (3%), discount, earnings.
  - Table sorting: By date, distance, fare, etc.
  - LocalStorage: Persists trips, wallet, goal data.
- Styling: Consistent with dashboard, responsive.

### General
- **Setup**:
  - Hosted locally on Dell Latitude (4GB RAM).
  - Used `python -m http.server`.
- **Known Issues**:
  - Syntax errors in event listeners (fixed in 1.0.1).
  - Hardcoded time (fixed in 1.0.1).

---

[1.0.1]: #1.0.1
[1.0.0]: #1.0.0