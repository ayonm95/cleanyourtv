# CleanYourTV Progress Tracker

## Project Overview
Custom native Android TV launcher (`com.gathin.tvhome`) deployed on Sony Bravia 4K TV (`BRAVIA_VU31_4K`). Features an authentic minimalist CleanYourTV interface, hardware HDMI 3 PlayStation 5 passthrough, debloated system telemetry and background ad services for maximum RAM efficiency (530MB free), and full hardware remote hotkey mapping.

---

## Milestone Timeline & Status
- **Overall Status**: Complete & Verified on Sony Bravia TV (`192.168.1.3:5555`)
- **Active Branch**: `main`

---

## Completed Features & Tasks
- [x] **Revert UI to Original CleanYourTV Interface**:
  - Removed custom injected `ps5Panel` from `activity_main.xml` and `MainActivity.java`, restoring the unhindered clean top shelf hero header (`heroName`, `heroSub`, `heroDots`).
  - Restored squircle card background (`#FF1C1C1E`, 16dp corner radius) in `tile_bg.xml` and restored memory-efficient banner card drawing in `AppAdapter.java`.
  - Restored authentic app banners for streaming services (Netflix, Amazon Prime Video, Disney+ Hotstar, YouTube, Spotify, Apple TV) loaded directly from their installed packages, with an official PlayStation 5 banner mapped to HDMI 3.
  - Restored the original, serene Mount Fuji twilight wallpaper (`01-fuji-twilight.jpg`) with frosted dock container (`dock_glass: true`, `dock_band_all: true`, `dock_opacity: 60`, `wallpaper_dim: 25`).
- [x] **Keep Strictly User-Requested Apps in Dock**:
  - Isolated the home screen dock to exclusively the 7 apps requested by the user:
    1. **PlayStation 5**: Mapped to hardware HDMI 3 passthrough (`input:com.realtek.tv.passthrough/.hdmiinput.HDMITvInputService/HDMI300004`) via `launch_actions`.
    2. **Netflix**: `com.netflix.ninja`
    3. **Amazon Prime Video**: `com.amazon.amazonvideo.livingroom`
    4. **Disney+ Hotstar**: `in.startv.hotstar`
    5. **YouTube**: `com.google.android.youtube.tv`
    6. **Spotify**: `com.spotify.tv.android`
    7. **Apple TV**: `com.apple.atve.androidtv.appletv`
  - Added all other non-dock leanback apps to `hidden_apps`, ensuring the home screen remains completely uncluttered and single-row.
- [x] **Sony Bravia VU3 System Debloating & Memory Optimization**:
  - Disabled 18 bloatware, telemetry, in-store demo, and background ad services on the TV (`192.168.1.3:5555`):
    - `com.sony.dtv.promos` (Sony BRAVIA promos)
    - `com.sony.dtv.sonyselect` (Sony Select)
    - `com.sony.dtv.sonytab` (Sony content tab)
    - `com.sony.dtv.multiscreendemo` (In-store demo)
    - `com.sony.dtv.smarthelp` (Sony help tile)
    - `com.sony.dtv.helpguidecontents` (Help guide content)
    - `com.sonypicturescore` (Sony Pictures Core preload)
    - `com.android.adservices.api` (Privacy Sandbox ad services)
    - `com.android.federatedcompute.services` (Federated compute services)
    - `com.android.ondevicepersonalization.services` (On-device personalization)
    - `com.google.android.feedback` (Google feedback reporter)
    - `com.google.android.partnersetup` (Partner setup/attribution)
    - `com.google.android.onetimeinitializer` (One-time setup initializer)
    - `com.google.android.syncadapters.calendar` (Calendar sync adapter)
    - `com.android.printspooler` (Print service)
    - `android.autoinstalls.config.google.gtvpai` (Google TV partner auto-installs)
    - `com.android.gallery3d` (Legacy gallery app)
    - `com.google.android.apps.tv.dreamx` (Ambient screensaver)
  - Force-stopped inactive daemons to immediately reclaim system RAM.
  - Increased available system RAM from ~411MB to 530MB on the 2GB device (`MemAvailable: 529568 kB`).
- [x] **Sony Remote Hardware Hotkeys Preservation**:
  - Handled remote hotkey dispatch across both foreground window (`MainActivity.dispatchKeyEvent`) and system-wide accessibility service (`HomeKeyService.onKeyEvent`):
    - **Netflix Hotkey**: Handled `KEYCODE_BUTTON_4` (191), `KEYCODE_BUTTON_1` (188), vendor key `4062`, and Sony scancode `758`, launching `com.netflix.ninja`.
    - **All Apps ("LL" / APPS) Hotkey**: Handled `KEYCODE_ALL_APPS` (284) and `KEYCODE_WINDOW` (171), launching the full leanback App Library overlay (`FullscreenAppsActivity`).
    - **Settings Hotkey**: Handled `KEYCODE_SETTINGS` (176), `KEYCODE_MENU` (82), notification quick settings (`83`), `KEYCODE_QUICK_SETTINGS` (177), and `KEYCODE_HELP` (259), launching Sony's native Quick Settings ribbon with fallback to Android TV Settings (`android.settings.SETTINGS`).
    - **Prime Video Hotkey**: Handled `KEYCODE_BUTTON_2` (189), `KEYCODE_BUTTON_5` (195), and Sony scancodes `652` / `490`, launching `com.amazon.amazonvideo.livingroom`.
    - **YouTube Hotkey**: Handled `KEYCODE_BUTTON_14` (200), `KEYCODE_BUTTON_3` (190), and Sony scancodes `569` / `485`, launching `com.google.android.youtube.tv`.
    - **Disney+ Hotstar Hotkey**: Handled `KEYCODE_BUTTON_15` (201) and Sony scancodes `653` / `491`, launching `in.startv.hotstar`.
    - **TV / Input Switcher**: Handled `KEYCODE_TV` (170), `KEYCODE_TV_INPUT` (178), and `KEYCODE_BUTTON_10` (197).

---

## Verified Scenarios
- [x] Verified native release APK compilation (`assembleRelease`): `BUILD SUCCESSFUL in 19s`.
- [x] Verified live deployment via wireless ADB to Sony Bravia TV at `192.168.1.3:5555`.
- [x] Verified live screen state via hardware screencap (`docs/screen_restored_clean.png`):
  - Clean Mount Fuji twilight wallpaper with frosted glass dock band.
  - Exactly 7 tiles: PlayStation 5, Netflix, Prime Video, JioHotstar, YouTube, Spotify, Apple TV.
  - Clean top bar with time, date, crescent moon divider, and quick pills (Inputs, Wi-Fi, Settings).
- [x] Verified system memory increase via `cat /proc/meminfo`:
  - `MemTotal: 2,097,152 kB`
  - `MemAvailable: 529,568 kB` (up from 438,848 kB).
- [x] Verified remote hotkey execution over ADB:
  - Netflix key (`KEYCODE_BUTTON_4` 191) opens `com.netflix.ninja`.
  - Settings key (`KEYCODE_SETTINGS` 176) opens Settings.
  - All Apps key (`KEYCODE_ALL_APPS` 284) opens `FullscreenAppsActivity`.
