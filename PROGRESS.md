# CleanYourTV Progress Tracker

## Project Overview
Custom native Android TV launcher (`com.gathin.tvhome`) deployed on Sony Bravia 4K TV (`BRAVIA_VU31_4K`) with Apple-inspired Liquid Glass interface, hardware HDMI 3 input integration, PS5 minimalistic game widget, and ultra-sharp 4K Vice City Atlantic Hotel sunset wallpaper.

---

## Milestone Timeline & Status
- **Overall Status**: Complete & Live on Sony Bravia TV (`192.168.1.3:5555`)
- **Active Branch**: `main`

---

## Completed Features & Tasks
- [x] **Complete Sony Remote Hotkey Integration (Netflix, All Apps, Settings, Prime, YouTube, Hotstar)**:
  - Fixed remote hotkey dispatch across both foreground window (`MainActivity.dispatchKeyEvent`) and system-wide accessibility service (`HomeKeyService.onKeyEvent`):
    - **Netflix Hotkey**: Handled `KEYCODE_BUTTON_4` (191), `KEYCODE_BUTTON_1` (188), vendor key `4062`, and Sony scancode `758`, launching `com.netflix.ninja`.
    - **All Apps ("LL" / APPS) Hotkey**: Handled `KEYCODE_ALL_APPS` (284) and `KEYCODE_WINDOW` (171), launching the full leanback App Library overlay (`MainActivity.ACTION_APP_LIBRARY`).
    - **Settings Hotkey**: Handled `KEYCODE_SETTINGS` (176), `KEYCODE_MENU` (82), notification quick settings (`83`), `KEYCODE_QUICK_SETTINGS` (177), and `KEYCODE_HELP` (259), launching Sony's native Quick Settings ribbon (`com.sony.dtv.smartui/.settings.SmartSettingsActivity`) with fallback to Android TV Settings (`android.settings.SETTINGS`).
    - **Prime Video Hotkey**: Handled `KEYCODE_BUTTON_2` (189), `KEYCODE_BUTTON_5` (195), and Sony scancodes `652` / `490`, launching `com.amazon.amazonvideo.livingroom`.
    - **YouTube Hotkey**: Handled `KEYCODE_BUTTON_14` (200), `KEYCODE_BUTTON_3` (190), and Sony scancodes `569` / `485`, launching `com.google.android.youtube.tv`.
    - **Disney+ Hotstar Hotkey**: Handled `KEYCODE_BUTTON_15` (201) and Sony scancodes `653` / `491`, launching `in.startv.hotstar`.
    - **TV / Input Switcher**: Handled `KEYCODE_TV` (170), `KEYCODE_TV_INPUT` (178), and `KEYCODE_BUTTON_10` (197).
- [x] **Clean PS5 Widget & Glow Removal**:
  - Removed garish neon halo underglow (`bg_ps5_ambient_glow.png`) and rainbow gradient rim (`bg_ps5_gradient_border.png`) per user feedback.
  - Sized `ps5Panel` (168dp x 105dp) as a clean, razor-sharp squircle card with 20dp corner radius (`setClipToOutline(true)`), 4dp resting hardware elevation shadow, and smooth 1.08x focus zoom without visual clutter.
  - Retained the high-contrast DualSense controller vector glyph and battery capsule at bottom-right.
- [x] **Official Sony DualSense Controller Glyph (`ic_dualsense_subtle.xml`)**:
  - Replaced legacy distorted path with an authentic, production-grade Sony PlayStation UI DualSense controller vector glyph.
  - Features iconic DualSense architecture:
    - Pure white ergonomic outer shell (`#FFFFFF`) with flared grips and smooth palm curves.
    - Two-tone dark obsidian chin and analog bridge (`#151821`).
    - Wide trapezoidal touchpad (`#1D222E`).
    - Vice City glowing lightbar perimeter in Electric Cyan (`#00F0FF`, stroke 0.9dp).
    - Twin symmetrical analog thumbsticks (`#0E1017` / `#242B38`).
    - High-contrast D-pad directional cross (`#1E232F`).
    - 4 action buttons with neon accents (Cyan & Magenta).
    - Official PlayStation center Home button (`#00F0FF`).
  - Seamlessly embedded in the Liquid Glass battery pill capsule (`bg_battery_capsule.xml`) alongside refined battery level and percentage.
- [x] **Refined Battery Indicator (`ic_battery_subtle.xml`) & Pill Capsule (`bg_battery_capsule.xml`)**:
  - Re-engineered horizontal battery vector (20x12 viewport, 15x10dp) with zero vertical dead-zones, high-contrast frame, positive terminal nipple, and 92% active fill in Electric Cyan (`#00F0FF`).
  - Styled translucent glass capsule (`#CC090314`) with 1dp glass stroke (`#4DFFFFFF`) and 14dp pill radius.
- [x] **Vice City Multi-Layer Gradient Glow for PS5 Tile (`ps5Panel`)**:
  - Transformed simple border into a rich multi-layer gradient glow system matching GTA VI Vice City neon sunset vibes:
    - Sunset Gold (`#FFE000`)
    - Neon Magenta (`#FF007A`)
    - Deep Violet (`#9A16FF`)
    - Electric Cyan (`#00F0FF`)
  - **Layer 1: Ambient Halo Underglow** (`bg_ps5_ambient_glow.png`, 760x540) radiating 49dp outward with smooth exponential Gaussian falloff ($e^{-(d/\sigma)^2}$, $\sigma=45\text{px}$) and dark center cutout so game art stays 100% crisp.
  - **Layer 2: 20dp Squircle Outline Clipping** (`setClipToOutline(true)`) for GTA VI key art.
  - **Layer 3: Specular Multi-Color Neon Rim & Glass Sheen** (`bg_ps5_gradient_border.png`, 672x420) with 2.5dp antialiased stroke inside the squircle and top glass specular sheen for Liquid Glass / Apple TV aesthetic.
  - **Coordinated Focus Bloom**: When focused via D-pad, tile expands to 1.08x, elevates to 14dp Z-translation, while ambient glow blooms to full 1.0f alpha at 1.15x scale in 200ms decelerate curve (`/apple-design`, `/reanimate`).
- [x] **4K Ultra-Sharp Zoomed-Out Wallpaper**: Enhanced Vice City Atlantic Hotel sunset illustration (`3840x2160`) using Lanczos-4 upscaling, bilateral denoising, and unsharp masking. Fixed `sky_intensity: 0` and `wallpaper_dim: 0` to preserve full vibrant pastel sunset gradients.
- [x] **Apple Design & Liquid Glass Dock Tiles (`/apple-design`, `/liquidgl`)**:
  - Re-engineered `tile_bg.xml` into a frosted see-through glass shape with subtle top-to-bottom white gradient (`#2BFFFFFF` to `#08FFFFFF`) and 1px specular border (`#3DFFFFFF`).
  - Bundled high-res transparent vector banners for Netflix, Amazon Prime Video, Disney+ Hotstar, YouTube, Spotify, Apple TV, and PlayStation 5 (`banner_netflix`, `banner_prime`, `banner_hotstar`, `banner_youtube`, `banner_spotify`, `banner_appletv`, `banner_ps5`).
  - Updated `AppAdapter.java` to preserve the frosted glass background under transparent banners and icons, allowing the 4K wallpaper to shine seamlessly through every dock tile.
- [x] **Typography & Date/Time Hierarchy**:
  - Fixed time and date overlapping by enabling `"date_below_clock": true` and increasing AM/PM margins (`10dp`).
  - Upgraded font to `@string/font_medium` (Outfit Medium) with optical kerning (`letterSpacing="-0.01"`), rendering crisp, non-colliding typography.
- [x] **Remote Navigation Integration**:
  - Fluid D-Pad navigation between Top Buttons, PS5 Game Widget, and Dock Row.

---

## Verified Scenarios
- [x] Verified remote hotkey execution over ADB:
  - Netflix key (`KEYCODE_BUTTON_4` 191) opens `com.netflix.ninja/.MainActivity` immediately.
  - Settings key (`KEYCODE_SETTINGS` 176) opens `com.android.tv.settings/.MainSettings` immediately.
  - All Apps key (`KEYCODE_ALL_APPS` 284) opens `com.google.android.apps.tv.launcherx/.guide.home.moreapps.ui.FullscreenAppsActivity`.
- [x] Verified clean PS5 tile appearance via hardware screencap (`docs/screen_no_glow.png`): neon halo and gradient border completely removed, crisp 20dp squircle Lucia & Jason GTA VI card with subtle DualSense battery capsule.
- [x] Verified native APK compilation with OpenJDK 17 and Gradle 8.9 (`assembleRelease`): `BUILD SUCCESSFUL in 5s`.
- [x] Verified test suite passing: `./gradlew test` (40 tasks, `BUILD SUCCESSFUL in 5s`).
- [x] Verified live deployment via wireless ADB to Sony Bravia TV at `192.168.1.3:5555`.
- [x] Verified live screen state via `screencap` in resting and focused states (`docs/screen_gtavi_glow.png` and `docs/screen_gtavi_glow_focused.png`).
- [x] Verified D-Pad navigation between dock and PS5 widget without animator cancellation stutter or visual clipping.
