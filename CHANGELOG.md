# Changelog

All notable changes to this fork of GAS-ICS-Sync will be documented in this file.

## [5.9] - 2025-05-05

### Fixed

- **Weekly reminders silently zeroed**: Bitwise AND (`&`) was used instead of multiplication (`*`) in `parseNotificationTime`, causing weekly notification times to always resolve to 0 minutes.
- **DELEGATED attendee status dropped**: `indexOf` returning 0 for the first element ("DELEGATED") was treated as falsy, causing delegated attendees to be set to null instead of "tentative".
- **Backoff jitter never applied**: Misplaced parenthesis in `callWithBackoff` caused the random jitter to be computed but discarded instead of added to the sleep duration.
- **Race condition in concurrency guard**: Replaced the TOCTOU (time-of-check-time-of-use) `LastRun` property check with `LockService.getUserLock()` and `try/finally`, preventing overlapping sync runs and ensuring the lock is always released.
- **"Invalid start time" on recurring events**: Added filtering of cancelled events from fetched `calendarEvents` to prevent errors when updating recurring event instances.
- **Operator precedence in trigger frequency validation**: `!origFrequency > 0` evaluated as `(!origFrequency) > 0` instead of `!(origFrequency > 0)`.
- **Unnecessary String.prototype.includes polyfill**: Removed polyfill that was overriding the native V8 implementation.
- **Duplicate variable declaration**: Removed duplicate `var subject` in `sendSummary`.
- **Extra argument in updatePropertyWithValue**: Removed the third unused `Utilities.Charset.UTF_8` argument.

### Added

- **cleanupDuplicates utility**: New `cleanupDuplicates()` function to safely remove all script-created events (tagged with `fromGAS=true`) from a specified calendar. Requires explicitly setting `calendarToCleanup` variable before running to prevent accidental execution.

### Credits

- Concurrency fix inspired by PR [#504](https://github.com/derekantrican/GAS-ICS-Sync/pull/504) by @pedrocarvalhlima
- Cancelled events filter inspired by PR [#520](https://github.com/derekantrican/GAS-ICS-Sync/pull/520) by @claw-56k

## [5.8] - 2024-10-28

- Upstream release by @derekantrican / @jonas0b1011001
- See https://github.com/derekantrican/GAS-ICS-Sync/releases for prior history
