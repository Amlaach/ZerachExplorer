# Changelog

All notable changes to ZerachExplorer will be documented in this file.

## [1.6.0] - Stage 3: Admin Profiles & Policy Configuration Engine

### Features & Security (תכונות חדשות ואבטחה)
- **Kiosk Operational Profiles (פרופילי עמדה מובנים):** Introduced built-in presets: Standard Documents Kiosk, Read-Only Kiosk (blocks writing, deleting, renaming, and folder creation), Controlled Workstation (restricts operations to explicitly allowed directories), and Custom profiles.
- **Granular Action Permissions (מודל הרשאות פעולה מפורט):** Added granular permission flags (`CanList`, `CanOpen`, `CanCopyFrom`, `CanCopyTo`, `CanRename`, `CanDelete`, `CanCreateDirectory`) enforced throughout `PathPolicy` and reflected dynamically in the UI command bar (`CanExecute`).
- **Protected Configuration Service (שירות תצורה מוגן ב-ProgramData):** Implemented `IConfigurationService` managing JSON configuration under `%ProgramData%\ZerachExplorer\config.json` with fallback handling and secure ACL preservation for kiosk environments.
- **PBKDF2 Password Security (אבטחת סיסמה בהצפנת תקן):** Added `SecurityHelper` utilizing PBKDF2 (SHA-256 with 10,000 iterations and cryptographic salts) to secure administrator access.
- **Admin Password Authentication Dialog (דיאלוג אימות סיסמת מנהל):** Created modern modal password prompt protecting administrative operations.
- **Admin Settings Management Window (מסך ניהול והגדרות מנהל):** Added full-featured administration dialog accessible via toolbar and keyboard shortcut (`Ctrl+Shift+A`) allowing real-time editing of active profiles, permissions, allowed file extensions, explicit directories, and password changes.

### Testing (בדיקות)
- **Stage 3 Verification:** Added unit tests verifying password hashing and verification, configuration JSON persistence and round-trip, profile policy enforcement (ReadOnly, Controlled, Custom), and dynamic policy application.

## [1.5.1] - Tabs UX & Color Palette Improvements

### Features & UI (תכונות וממשק משתמש)
- **Tab Close Button (איקס לסגירת כרטיסיות):** Added a close ('X') button to explorer tabs matching modern browser and Windows Explorer behaviors with proper RTL alignment, hover cursor, and graceful exit upon closing the last active tab.
- **Color Palette Brightening (הבהרת גווני כתום):** Brightened the dark rust-orange warning and danger palette in PercentToColor converter to clear, vibrant tones (RGB(255, 140, 20) and RGB(255, 185, 60)).

## [1.5.0] - Stage 2: File Operations & Device Management

### Features (תכונות חדשות)
- **File Copy & Paste (העתקה והדבקה):** Added clipboard copy and paste (Ctrl+C / Ctrl+V) with double `PathPolicy` security validation across both source and destination paths.
- **File Cut & Move (גזירה והעברה):** Added clipboard cut and move (Ctrl+X / Ctrl+V) with permission checks for reading, destination writing, and source deletion.
- **Multi-Item Selection (בחירה מרובה):** Extended selection support allowing batch copy, cut, and deletion across multiple selected items.
- **New Folder Creation (יצירת תיקייה חדשה):** Added toolbar button, context menu item, hotkey (Ctrl+Shift+N), and modal input dialog with validation against reserved DOS names and illegal characters.
- **Conflict Resolution Dialog (פתרון התנגשויות קבצים):** Added interactive resolution dialog (Replace, Skip, Keep Both / Auto-rename) with batch "Apply to all" support.
- **Safe USB Ejection (הוצאה בטוחה של התקני USB):** Implemented `DriveEjectService` using Windows Storage IOCTLs to lock, dismount, and safely eject removable media with user notifications in Hebrew.

### Testing (בדיקות)
- **Stage 2 Verification:** Added unit tests covering copy and move policies, directory creation checks, device ejection restrictions, and conflict resolution models.
