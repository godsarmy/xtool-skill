---
name: xtool-ios-build
description: Build and deploy iOS apps with xtool in SwiftPM-based projects, including setup, project structure, and troubleshooting.
license: MIT
compatibility: opencode
metadata:
  audience: ios-developers
  workflow: cli
---

# xtool iOS Build Skill

## What this skill does

- Guides setup for xtool on Linux/WSL and macOS.
- Provides a repeatable compile/build/install workflow for iOS apps.
- Documents required project structure (`Package.swift` + `xtool.yml`).
- Covers `xtool.yml` controls for bundle metadata, resources, icons, and entitlements.
- Includes common failure modes and concrete recovery steps.

## When to use

Use this skill when you need to compile, package, sign, and install an iOS app using `xtool` in a SwiftPM-based project.

## Preconditions

- You have a SwiftPM iOS app project (or will create one with `xtool new`).
- You have a physical iOS device connected for install/test flow.
- You can authenticate to Apple services during `xtool setup`.

## Setup

### Linux / WSL

1. Install Swift 6.2 and verify:

```bash
swift --version
```

2. Install USB plumbing:

```bash
sudo apt update
sudo apt install usbmuxd
```

Optional diagnostics:

```bash
sudo apt install libimobiledevice-utils
ideviceinfo
```

3. Download `Xcode.xip` from Apple Developer downloads in a browser.
4. Install xtool and verify:

```bash
xtool --help
```

5. Run initial setup:

```bash
xtool setup
```

6. Verify iOS Swift SDK installation:

```bash
swift sdk list
```

### macOS

1. Install Xcode.
2. Verify iOS SDK path:

```bash
xcrun -sdk iphoneos -show-sdk-path
```

3. Install xtool and verify:

```bash
xtool --help
```

4. Run setup:

```bash
xtool setup
```

## Authentication mode guidance

- Prefer **API Key** mode when enrolled in paid Apple Developer Program (recommended by docs).
- Use **Password** mode if API Key is not available.

## Standard build workflow

### 1) Create or open project

Create a fresh project:

```bash
xtool new Hello
cd Hello
```

Generated files include:

- `Package.swift`
- `xtool.yml`
- `.sourcekit-lsp/config.json`

### 2) Build and install to connected device

```bash
xtool dev
```

What `xtool dev` handles:

- Build using SwiftPM iOS cross-compilation.
- Provision/sign package.
- Install app to connected iPhone.

Note: first run can be significantly slower due to cold module compilation; subsequent runs are faster with cache reuse.

### 3) Iterate

- Edit code.
- Re-run `xtool dev`.
- Validate behavior on device.

## Required project structure

At minimum:

- SwiftPM manifest: `Package.swift`
- xtool control file: `xtool.yml`

Minimal `xtool.yml`:

```yaml
version: 1
bundleID: com.example.Hello
```

## `xtool.yml` controls

- `bundleID`: base app bundle identifier.
- `infoPath`: merge/override selected `Info.plist` keys.
- `resources`: copy files into app bundle root.
- `iconPath`: app icon path (PNG, ideally 1024x1024).
- `entitlementsPath`: entitlements plist path.

Example:

```yaml
version: 1
bundleID: com.example.Hello
infoPath: App-Info.plist
iconPath: Icon.png
resources:
  - GoogleServices-Info.plist
entitlementsPath: App.entitlements
```

## App Extensions workflow

For widget/extensions, define main product and extension products in `xtool.yml`:

```yaml
version: 1
bundleID: com.example.Hello
product: Hello
extensions:
  - product: HelloWidget
    infoPath: HelloWidget-Info.plist
```

## Troubleshooting checklist

- Device trust prompt appeared and install failed:
  - Accept trust on device, then rerun `xtool dev`.
- Developer Mode disabled:
  - Enable Developer Mode on iOS device and retry.
- "Untrusted Developer" on launch:
  - Trust profile in iOS Settings, then relaunch app.
- Device not detected in Linux/WSL:
  - Confirm USB passthrough/binding and run `ideviceinfo`.
- Entitlements not applied:
  - Verify capability support and account limitations.

## Build output inspection

After build/install, inspect packaged app in:

- `./xtool/<AppName>.app`

Use this to verify merged `Info.plist`, copied resources, and expected bundle contents.

## References

- https://xtool.sh/documentation/xtool/
- https://xtool.sh/documentation/xtool/installation-linux/
- https://xtool.sh/documentation/xtool/installation-macos/
- https://xtool.sh/tutorials/xtool/first-app/
- https://xtool.sh/documentation/xtool/control/
- https://xtool.sh/documentation/xtool/appex/
