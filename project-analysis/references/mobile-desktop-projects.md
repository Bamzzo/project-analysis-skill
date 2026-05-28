# Mobile and Desktop Project Analysis

Use this reference for Android, iOS, Flutter, React Native, Electron, Tauri, desktop webview, or native desktop projects.

## First Questions

- What platforms are targeted: Android, iOS, macOS, Windows, Linux, web, or mixed?
- What is native shell code and what is shared application code?
- Where are the app entrypoints, navigation roots, and platform lifecycle hooks?
- What permissions, entitlements, deep links, background modes, or native capabilities are used?
- How does the app store local state, credentials, cache, and user preferences?
- How are development, debug, staging, production, and release builds configured?
- How is the app packaged, signed, and distributed?

## Components to Locate

- Android: `AndroidManifest.xml`, Gradle files, `MainActivity`, `Application`, permissions, flavors, signing config.
- iOS/macOS: `Info.plist`, entitlements, `AppDelegate`, `SceneDelegate`, SwiftUI `App`, Xcode project/workspace, schemes.
- Flutter: `pubspec.yaml`, `lib/main.dart`, platform folders, method channels, build flavors.
- React Native/Expo: `package.json`, `app.json`/`app.config.*`, `index.*`, native modules, Metro config, EAS or native build config.
- Electron: main process, preload scripts, renderer app, IPC channels, packaging config.
- Tauri: `tauri.conf.*`, Rust commands, frontend app, permissions/capabilities, sidecar binaries.
- Shared app layers: routing/navigation, state management, API clients, persistence, error reporting, analytics, update mechanism.

## Runtime Flow Patterns

Mobile/native:

```text
platform launch
-> native lifecycle hook
-> app root/navigation
-> screen/view model/state
-> service/API/persistence/native bridge
-> UI update or platform side effect
```

Electron/Tauri:

```text
desktop process
-> main/native runtime
-> preload/bridge or command registry
-> renderer UI
-> IPC/native command/API client
-> filesystem/network/OS side effect
```

## Common Failure Modes

- Debug and release builds use different API endpoints or permissions.
- Native bridge contracts are implicit or weakly typed.
- Platform lifecycle events race with async initialization.
- Local storage or keychain access differs by platform/version.
- Deep links, push notifications, background tasks, or file associations are configured in multiple places.
- Desktop preload/IPC exposes too much authority to renderer code.
- Build signing, provisioning, or app identifiers are undocumented.
- Packaged app behavior differs from dev-server behavior.

## Verification

Prefer:

- inspect platform manifests/configs before running builds
- run typecheck/unit tests for shared code
- run platform lint or configuration checks when available
- launch a simulator/emulator/dev build only when dependencies are ready and safe
- verify one navigation/API/native-bridge smoke path
- inspect packaging/signing workflows without publishing

## Recommended Output Additions

For mobile or desktop projects, add:

1. Platform Target Map
2. Native vs Shared Code Boundary
3. Lifecycle and Navigation Entry Points
4. Permission, Entitlement, and Native Capability Map
5. Local State and Secure Storage
6. Build, Signing, and Distribution Path
7. Platform-Specific Risks
