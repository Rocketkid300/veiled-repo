# Veiled — Changelog

## [2.0.0] — 2026-10-05

First public release of Veiled 2. Tested on iPhone 7 Plus (A10), iOS 15.8.3,
Dopamine rootless.

### App (now a Calculator)
- Shows as **Calculator** on the Home Screen: a working calculator styled like
  current iOS. Type your passcode and press **=** to open Veiled.
- Hidden-app list: tap to open, swipe to unhide, **+** to hide several apps at
  once, search, and a Recent section.
- Notes rebuilt: full-screen editor, pinning, search, optional **Lock Notes**
  (Touch ID or passcode).
- **Backup & Restore**: hidden list + notes, encrypted with your passcode.
- **Auto-Lock**, **duress code** (opens an empty list), iOS-style Settings.
- Fixed: black screen after unlocking, codes longer than 4 digits, the keypad
  delete key, Unhide All available without a code in the calculator.

### Tweak
- **Close on Lock**: Calculator and hidden apps close 5 seconds after the phone
  locks (switch in Settings).
- **Low-battery reminder** at 15%: reminds you to re-jailbreak if the phone
  turns off, so your apps stay hidden. Shown only while unlocked.
- Model-level hiding hooks install reliably even when SpringBoard loads late.
- Installing the tweak now also installs the app.

## [1.0.0] — 2026-09-28

### Changed
- **Rebranded Hidden Folder → Veiled.** New bundle IDs `com.rocketkid300.veiled`
  (tweak) and `com.rocketkid300.veiledvault` (app; renamed to `com.rocketkid300.veiled.app` in v2), new prefs domain
  `com.rocketkid300.veiled`, new Darwin notification
  `com.rocketkid300.veiled.settingschanged`, binaries `Veiled.dylib` / `Veiled`,
  log prefix `[Veiled]`. Versions reset to 1.0.0 (new IDs = a fresh package line,
  not a downgrade of the old one).

### Added
- **One-time migration from the old identity.** On first run of either binary,
  the prefs-resident data (`HiddenApps`, `HiddenNotes`, `Enabled`,
  `UseSystemAuth`) is copied once from `com.bigpickle.hiddenfolder`, guarded so it
  never clobbers data the new build already wrote. The passcode and duress
  code live in the keychain (not prefs); a read-through fallback reads them from
  the old keychain service/account and writes them into the new identity on first
  use. If the new bundle identity cannot read the old keychain item, the app says
  so explicitly instead of silently offering "set a passcode".

Notes below this line predate the rename and refer to the old identifiers.

---

## [2.3.3] — 2026-09-21

### Fixed
- **Main-Thread LaunchServices Deadlock**: Resolved UI hang caused by synchronous `allApplications` lookups and icon decoding on the main runloop by moving fetch operations to background queues with a loading state (`HV2Apps`).
- **Safe KVC Evaluation**: Added `HV2SafeValue` safety checks around `valueForKey:` calls to prevent SIGABRT crashes on unrecognized app keys.

---

## [2.0.9] — 2026-09-21

### Fixed
- banner removal (all calls, logs kept)
- hide-every-instance traversal
- relaunch re-sanitize
- protected-ID refusal + self-heal
- removed unevidenced search/share/widget filter hooks (no fake coverage claimed)