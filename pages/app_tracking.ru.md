---
title: Как отслеживаются приложения
description: Как отслеживаются приложения в Obtainium
---

# Как отслеживаются приложения

## Основные положения

Когда вы добавляете URL-адрес приложения в Obtainium, вы должны выбрать [источник](sources.md). Источники определяют, как информация о приложении и APK-файлы будут извлечены из введенного вами URL. В большинстве случаев Obtainium автоматически выбирает подходящий источник для использования - если это невозможно, появится выпадающий список «Переопределить источник».

Источники приложений должны предоставлять как минимум следующие данные для своих приложений:

- Версия приложения (или «псевдо-версия» - идентификатор, который меняется для каждой новой версии приложения)
- По крайней мере один URL-адрес загрузки соответствующий предоставленной версии APK

Источники приложений могут предоставлять и другую информацию - она позволяет использовать дополнительные функции или преимущества пользовательского интерфейса. Например:

- Имя автора приложения
- ID пакета приложения
- Дата выхода последней версии
- Информация о предыдущих версиях или вариантах приложения

В идеальном мире каждый источник приложений мог бы предоставлять всю необходимую информацию в стандартном формате и простым способом - по одному приложению на заданный URL-адрес. Однако часто это не так - существует множество различных способов обработки релизов приложений, даже из одного и того же источника, поэтому невозможно создать фиксированный набор шагов для их обработки. По этой причине при добавлении приложения вам предлагается несколько дополнительных опций, которые можно использовать для изменения способа извлечения информации о приложении. Хотя для большинства приложений будут работать параметры по умолчанию, вы можете захотеть разобраться в этих опциях, чтобы справиться с нестандартными ситуациями - дополнительную информацию см. в разделе [Источники Приложений](sources.md) ниже.

Примечание: Многие настройки фильтров в Obtainium (включая многие опциональные фильтры для конкретного источника) используют [регулярные выражения](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) - вы должны быть знакомы с ними.

## Version Detection

When Obtainium is tracking an app that is currently installed, it grabs the version of the app from Android and compares it to the version string provided by the source. It then compares the two to decide whether an update is available or whether the install status of the app has changed. This comparison can only be made if the two versions follow the same format, which may not always be the case. For example, you could have any of these cases among others:

1. [Obtainium](https://github.com/ImranR98/Obtainium/releases/tag/v0.14.21-beta) from GitHub:

    - **Android-reported app version:** `0.14.21`
    - **Source-reported version:** `v0.14.21-beta` 

2. [Cheogram](https://git.singpolyma.net/cheogram-android/refs/2.12.8-2) from a SourceHut instance:

    - **Android-reported app version:** `2.12.8-2+free`
    - **Source-reported version:** `2.12.8-2`

3. [Tor](https://www.torproject.org/download/) from the Tor website:

    - **Android-reported app version:** `102.2.1-Release (12.5.6)`
    - **Source-reported version:** none (no version string is provided by this HTML source so a URL hash is used instead as a 'pseudo-version')

4. [Quotable](https://github.com/Lijukay/Qwotable/releases/tag/v10) from GitHub:

    - **Android-reported app version:** `1`
    - **Source-reported version:** `v10`

Obtainium stores a list of "standard" formats which it uses to make this comparison (like `x.y.z` or `x.y`). If both versions being compared conform to the same format, the comparison will be made. If not, version detection will be disabled for that app. In some cases, Obtainium will strip off extra parts from the source string if doing so would result in a standard version (like how `v` and `-beta` are removed from Obtainium's `v0.14.21-beta`), then it can make the comparison. We never try to strip parts off the "real" OS-provided version.

[This piece of code](https://github.com/ImranR98/Obtainium/blob/main/lib/providers/apps_provider.dart#L64) defines how the various "standard" formats are generated.

It's always possible to expand that code to add support for more formats, but this requires careful consideration. For example if Android reports that an installed app's version is `1.2` but the source says the latest available version of that app is `1.2-4`, should we strip off the `-4` and say the two are the same (meaning there is no update available)? This may be fine in some contexts (where the `-4` is not actually indicative of a change in the app itself) but not in other contexts. So it wouldn't be a good idea to support that specific case.

Version detection being turned off should not usually have a significant impact on day-to-day use. If version detection is disabled for an app, you may occasionally run into inconsistencies between the real version of the app installed on your system and the version shown in the Obtainium UI. This should only happen in two cases:

1. If an app's version changes due to actions taken outside of Obtainium (for example if it gets updated by Google Play)
2. If an attempt by Obtainium to [silently update](#background-updates) the app in the background fails

In such cases, Obtainium would not be able to detect that the app's real OS version has changed and so it would not update its internal records accordingly - you would need to manually correct the inconsistency.

See also: [Obtainium Issue #946 Comment](https://github.com/ImranR98/Obtainium/issues/946#issuecomment-1741745587)

## Background Updates

Obtainium checks for app updates in the background on a regular basis. You can control the frequency of these update tasks on the settings page.

After a background update checking task is completed, any available updates are divided into 2 categories:

1. Updates that can be applied in the background
2. Updates that cannot be applied in the background

For an update to be automatically installed in the background (AKA a silent update), certain criteria should be met:

- The OS must be Android 12 or higher
- The app being installed must target a [recent Android API level](https://developer.android.com/reference/android/content/pm/PackageInstaller.SessionParams#setRequireUserAction(int))
- The currently installed version of the app must have been installed by Obtainium
- You must have background updates enabled in Obtainium (both universally and for this app in particular - this is the default)
- If there are multiple APKs available for the update, the additional options for that app must be configured such that Obtainium can filter these down to one APK

Each available update is downloaded and installed if possible, and the user is then notified either of the update's availability or that it was installed in the background.

Note that due to technical limitations, background updates can only be installed on an asynchronous, best-effort basis. So if a background update fails to install, you will not be notified of the error.
