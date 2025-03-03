---
title: Wie Apps nachverfolgt werden
description: Wie Apps in Obtainium nachverfolgt werden
---

# Wie Apps nachverfolgt werden

## Grundlagen

Wenn Sie eine App-URL zu Obtainium hinzufügen, müssen Sie eine [App-Quelle](sources.md) auswählen. Quellen definieren, wie App-Informationen und APK-Dateien aus der von Ihnen eingegebenen URL extrahiert werden. In den meisten Fällen wählt Obtainium automatisch die entsprechende Quelle aus – um diese Auswahl zu korrigieren, wird ein Dropdown-Menü „Quelle überschreiben“ angezeigt.

Eine App-Quelle muss mindestens die folgenden Daten für ihre Apps bereitstellen:

- Die App-Version (oder eine „Pseudo-Version“ – eine Kennung, die sich bei jeder neuen Version der App ändert.)
- Mindestens eine APK-Download-URL, die der zur Verfügung gestellten Version entspricht

App-Quellen können auch andere Informationen liefern – diese ermöglichen zusätzliche Funktionen oder UI-Vorteile. Zum Beispiel:

- Der Name des Autors der Anwendung
- Die Package ID der Anwendung
- Das Veröffentlichungsdatum der neuesten Version
- Infos zu früheren Versionen oder Varianten der App

In einer idealen Welt würde jede App-Quelle alle erforderlichen Informationen auf unkomplizierte Weise bereitstellen - mit einer einzigen App pro angegebener URL, die alle erforderlichen Informationen in einem Standardformat enthält. Dies ist jedoch oft nicht der Fall – es gibt viele verschiedene Arten, wie App-Freigaben gehandhabt werden, sogar von derselben Quelle, so dass es nicht möglich ist, einen festen Satz von Schritten zu haben, um sie alle zu behandeln. Aus diesem Grund werden Ihnen beim Hinzufügen einer App verschiedene zusätzliche Optionen angeboten, mit denen Sie die Art und Weise, wie die App- Informationen extrahiert werden, ändern können. Während die Standardeinstellungen für die meisten Apps funktionieren, sollten Sie diese Optionen kennen, um mit Sonderfällen umgehen zu können – mehr dazu auf der Seite [App-Quellen](sources.md).

Hinweis: Viele Filtereinstellungen in Obtainium (einschließlich vieler quellenspezifischer optionaler Filter) verwenden [reguläre Ausdrücke](https://developer.mozilla.org/de/docs/Web/JavaScript/Guide/Regular_expressions) – Sie sollten mit diesen vertraut sein.

## Versionserkennung

Wenn Obtainium eine App trackt, die aktuell installiert ist, holt es sich die Version der App von Android und vergleicht sie mit der von der Quelle bereitgestellten Versionszeichenfolge. Dann vergleicht es die beiden, um zu entscheiden, ob ein Update verfügbar ist oder ob sich der Installationsstatus der App geändert hat. Dieser Vergleich kann nur durchgeführt werden, wenn die beiden Versionen das gleiche Format haben, was nicht immer der Fall ist. Es kann zum Beispiel einer der folgenden Fälle eintreten:

1. [Obtainium](https://github.com/ImranR98/Obtainium/releases/tag/v0.14.21-beta) von GitHub:

    - **Von Android gemeldete App-Version:** `0.14.21`
    - **Von der Quelle gemeldete Version:** `v0.14.21-beta` 

2. [Cheogram](https://git.singpolyma.net/cheogram-android/refs/2.12.8-2) von einer SourceHut-Instanz:

    - **Von Android gemeldete App-Version:** `2.12.8-2+free`
    - **Von der Quelle gemeldete Version:** `2.12.8-2`

3. [Tor](https://www.torproject.org/download/) von der Tor-Website:

    - **Von Android gemeldete App-Version:** `102.2.1-Release (12.5.6)`
    - **Von der Quelle gemeldete Version:** keine (diese HTML-Quelle liefert keine Versionszeichenfolge, daher wird stattdessen ein URL-Hash als „Pseudoversion“ verwendet)

4. [Quotable](https://github.com/Lijukay/Qwotable/releases/tag/v10) von GitHub:

    - **Von Android gemeldete App-Version:** `1`
    - **Von der Quelle gemeldete Version:** `v10`

Obtainium speichert eine Liste von „Standardformaten“, die es für diesen Vergleich verwendet (wie `x.y.z` oder `x.y`). Wenn beide zu vergleichenden Versionen demselben Format entsprechen, wird der Vergleich durchgeführt. Wenn nicht, wird die Versionserkennung für diese Anwendung deaktiviert. In einigen Fällen entfernt Obtainium zusätzliche Teile aus dem Quelltext, wenn dies zu einer Standardversion führen würde (wie z.B. `v` und `-beta` aus Obtainiums `v0.14.21-beta`), dann kann es den Vergleich durchführen. Wir versuchen nie, Teile der „echten“, vom Betriebssystem bereitgestellten Version zu entfernen.
