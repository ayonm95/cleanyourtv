# CleanYourTV Progress Tracker

## Project Overview
Custom native Android TV launcher (`com.gathin.tvhome`) deployed on Sony Bravia 4K TV (`BRAVIA_VU31_4K`) with Apple-inspired Liquid Glass interface, hardware HDMI 3 input integration, PS5 minimalistic game widget, and ultra-sharp 4K Vice City Atlantic Hotel sunset wallpaper.

---

## Milestone Timeline & Status
- **Overall Status**: Complete & Live on Sony Bravia TV (`192.168.1.3:5555`)
- **Active Branch**: `main`

---

## Completed Features & Tasks
- [x] **Official Sony DualSense Controller Glyph (`ic_dualsense_subtle.xml`)**:
  - Replaced legacy blocky gamepad with authentic Sony PlayStation UI controller vector glyph.
  - Modeled with precision DualSense silhouette: ergonomic flared handles, curved grip tips, wide center touchpad, twin symmetrical analog thumbsticks, D-pad, face buttons, and PS home button.
  - Active DualSense lightbar glowing in Vice City Electric Cyan (`#00F0FF`).
  - Seamlessly embedded in the Liquid Glass battery pill capsule (`bg_battery_capsule.xml`) alongside refined battery level and percentage.
- [x] **Vice City Multi-Layer Gradient Glow for PS5 Tile (`ps5Panel`)**:
  - Transformed simple 1dp border into a rich multi-layer gradient glow system matching GTA VI Vice City neon sunset vibes:
    - Sunset Gold (`#FFE000`)
    - Neon Magenta (`#FF007A`)
    - Deep Violet (`#9A16FF`)
    - Electric Cyan (`#00F0FF`)
  - **Layer 1: Ambient Halo Underglow** (`bg_ps5_ambient_glow.png`) radiating 22dp onto wallpaper with soft atmospheric lighting.
  - **Layer 2: 20dp Squircle Outline Clipping** (`setClipToOutline(true)`) for GTA VI key art.
  - **Layer 3: Specular Multi-Color Neon Rim & Glass Sheen** (`bg_ps5_gradient_border.png`) framing the card.
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
- [x] Verified native APK compilation with OpenJDK 17 and Gradle 8.9 (`assembleRelease`).
- [x] Verified live deployment via wireless ADB to Sony Bravia TV at `192.168.1.3:5555`.
- [x] Verified theme push via `tools/theme.sh themes/vice-city` with MD5 checksum verification.
- [x] Verified live screen state via `screencap` in resting and focused states (`docs/screen_gtavi_glow.png`).
