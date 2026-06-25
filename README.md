# Rescale

The missing menu for display scaling. Quick-switch display scaling from the
macOS menu bar — the same "Larger Text ↔ More Space" presets from System
Settings — as a two-click dropdown.

Built as a learning project to understand Swift, AppKit, CoreGraphics display
APIs, and the GitHub/CI development workflow.

## Requirements

- macOS 13 (Ventura) or later
- Apple Silicon or Intel Mac
- Swift 5.9+ (included with Xcode 15+ or the Swift toolchain)

## Build & Run

```bash
# Run from source (debug build)
swift run

# Build a .app bundle
./Scripts/make-app.sh
open Rescale.app
```

The app appears as a display icon in the menu bar with no Dock icon.

## How It Works

Rescale uses CoreGraphics to enumerate connected displays and their available
HiDPI scaled modes. It filters to a useful subset: modes matching the display's
native aspect ratio, from half-native resolution (2× retina, "Larger Text") up
to 1:1 native ("More Space"). A "Show All Resolutions" toggle reveals every
HiDPI mode the display supports.

See [docs/adr/](docs/adr/) for design decisions and the reasoning behind the
filtering approach.

## Project Structure

```
Package.swift                     # Swift Package Manager manifest
Sources/Rescale/
  main.swift                      # App entry point, menu bar UI
  DisplayManager.swift            # Display enumeration and mode filtering
Info.plist                        # macOS app bundle metadata (LSUIElement)
Scripts/
  make-app.sh                     # Assembles the .app bundle
.github/workflows/
  build.yml                       # CI — builds on every push and PR
docs/adr/
  0001-resolution-filtering.md    # Why we filter modes the way we do
```

## License

MIT
