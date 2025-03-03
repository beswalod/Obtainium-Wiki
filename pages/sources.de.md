---
title: App Sources
description: Information specific to certain sources
---

# App Sources

The way that an app is added, checked for updates, and installs will vary depending on source and the settings configured for that app by the user.

The following options are available for all apps regardless of source:

- Track-Only: Enabling this toggle allows you to receive update notifications for apps without attempting to actually download their APKs. This is useful to track updates for apps where no APKs are available, or where they cannot easily be extracted by Obtainium. Some sources are exclusively track-only - for example [ApkMirror](#apkmirror). Note that [version detection](app_tracking.md/#version-detection) will not work for any apps added as track-only.
- Version Detection: See the section on [version detection](app_tracking.md/#version-detection).
- Filter APKs by Regular Expression: When more than one APK is available for an app release, the user is prompted to pick one manually. Aside from being inconvenient, this means the app will not be updated silently in the background even when doing so would have otherwise been possible. This option lets the user specify a regular expression that can be used to filter out APK that don't match it (ideally down to one option).
- Attempt to filter APKs by CPU architecture if possible: This toggle will tell Obtainium to automatically filter out any APKs that don't appear to be compatible with the user's device. The logic used to do this is very simple and is based on the APK filename, so it is not always reliable and the user may still need to do their own filtering in many cases.
- App Name: This allows the user to specify their own name for the app instead of using the one Obtainium extracts.
- Exempt from background updates: This toggle will prevent the app from being updated silently in the background even if background updates are enabled and this app would otherwise have fulfilled all criteria to be updated in the background.
- Skip update notifications: This toggle tells Obtainium to avoid notifying the user that this app has an update available or that it was updated in the background.

Aside from those, each app has additional source-specific options. Most of those are self-explanatory and may be updated frequently, so they are not covered in this Wiki. However, some sources do have more unique behaviours that need more explanation, and these are covered below.

## Currently supported App sources

- Open Source - General:
    - [GitHub](https://github.com/)
    - [GitLab](https://gitlab.com/)
    - [Forgejo](https://forgejo.org/) ([Codeberg](https://codeberg.org/))
    - [F-Droid](https://f-droid.org/)
    - Third Party F-Droid Repos
    - [IzzyOnDroid](https://android.izzysoft.de/)
    - [SourceHut](https://git.sr.ht/)
- Other - General:
    - [APKPure](https://apkpure.net/)
    - [Aptoide](https://aptoide.com/)
    - [Uptodown](https://uptodown.com/)
    - [Huawei AppGallery](https://appgallery.huawei.com/)
    - [Tencent App Store](https://sj.qq.com/)
    - Jenkins Jobs
    - [APKMirror](https://apkmirror.com/) (Track-Only)
    - [RuStore](https://rustore.ru/)
- App-Specific:
    - [Telegram App](https://telegram.org)
    - [Neutron Code](https://neutroncode.com)
- Direct APK Link
- "HTML" (Fallback): Any other URL that returns an HTML page with links to APK files

## GitHub

GitHub puts a cap on the number of API requests you can make in a given period of time. Since Obtainium uses the GitHub API to grab release info, you may run into a "rate limit" error if you have more than a few dozen GitHub apps. You can get around this by getting a Personal Access Token.

GitHub also allows developers to host multiple releases of their app. This usually means older versions of the same app, but may also include pre-releases, variants, etc. - so Obtainium provides various filters that let you navigate this and grab the exact releases you are interested in.

- Some sources (like APKPure) may provide [XAPK files](https://apkpure.com/xapk.html) instead of APK files. Obtainium's XAPK support is incomplete and may not work reliably.
