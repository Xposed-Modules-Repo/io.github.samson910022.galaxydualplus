# Dual Clone Plus — BBC Helper (experimental beta)

Version: `0.1.0-beta.2` (versionCode `3`), signed single APK (companion app + LSPosed module), libxposed API 102, Samsung One UI / Android multi-user.

**Names:** the XMR module display name is "Dual Clone Plus — BBC Helper"; the installed app label is "Dual your Galaxy". They refer to the same signed APK under package `io.github.samson910022.galaxydualplus`.

**Identity notice — read before installing.** This Xposed-Modules-Repo release is the `io.github.samson910022.galaxydualplus` build. An earlier experimental build used `com.galaxydual.plus`; the two are **separate apps and separate LSPosed modules**. **Do not install or enable both at the same time.** Back up anything you care about, uninstall the old `com.galaxydual.plus` APK and disable its LSPosed module before installing this one. Both are experimental betas with the same disclosed limitations: Samsung may delete the dual clone and its data, the cause is unconfirmed, and this module makes **no data-safety guarantee**.

## What it does

- Authorization routing: ROOT (`su -c`) and Shizuku/ADB-shell command channels for `pm install-existing`, `pm uninstall`, `pm path` and related dual-profile operations. The app verifies the Dual Messenger profile identity (id/serial) before destructive actions and fails closed when identity is unknown.
- LSPosed BBC list extension: a hook on Samsung DAAgent's "available apps" query performs a union-only append of a user-edited BBC package set. The Stage-1 non-empty policy gate remains sealed; BBC injection is a separate experimental capability.
- Never touches Secure Folder (user 150), Knox, or SSAID settings. Scope is limited to `system` and `com.samsung.android.da.daagent`.

## ⚠️ Risks — read before installing

1. **Samsung may delete the dual clone and permanently erase its data.** In the 2026-11-23 A/B/C observation, the same Samsung system uid (`1000` / `android.uid.system:1000`) issued `START DELETE PACKAGE` for `com.openai.chatgpt` user 95 with BBC injection ON, with the runtime gate DB-confirmed OFF, and with this module's BBC hook entirely absent — always before any BBC callback. This is a **negative-control association**, not proof of a root cause and not a safety result. The pre-delete decision input inside Samsung `system_server` remains unmeasured.
2. **No data guarantee.** The maintainer accepted this as an **experimental limitation after honest disclosure — NOT a pass, NOT fixed, NOT safe**. If an App-caused unauthorized deletion is confirmed, it becomes a blocker again.
3. **Opt-out is NOT a deletion guard.** `BBC_AVAILABLE_APPS_INJECTION=true` and a missing runtime preference is treated as enabled. The hook may run before the first in-App warning; the App checkbox/dialog is **not** pre-activation consent.
4. **Root / Shizuku are operational routes, not backups.** Shizuku/ADB shell generally cannot back up another profile's private app data; `pm install-existing` restores package existence only, not erased chats, logins or private files. Having Root does not mean the Android Keystore or private data can be fully restored.
5. **BBC positive evidence is from older builds** (2026-11-17/18), **not from this version**; the effect is experimental / not device-verified on this version. Unverified ROM/version combinations are UNKNOWN / NOT VERIFIED. "Installed", "policy saved", and "BBC ON/OFF" do not mean "data safe".

**Back up important data using each app's own supported mechanism before use. Do not keep your only copy of important data inside a dual profile.**

## Installing / upgrading from the old package id

The applicationId and LSPosed module id changed to `io.github.samson910022.galaxydualplus`. This is a **fresh install under a new identity, not an in-place upgrade**. Channel preference, dual-app selection, risk-disclosure acknowledgement, repair hint and policy draft are **not migrated**; the old data remains under `com.galaxydual.plus` until you uninstall it. There is no in-app export/import — back up clone/chat data first. After installing, enable the module in LSPosed and (re)select scopes `system` and `com.samsung.android.da.daagent`.

## Links

- Source: https://github.com/samson910022/Dual-your-galaxy
- Issues / support: https://github.com/samson910022/Dual-your-galaxy/issues
- License: MIT
