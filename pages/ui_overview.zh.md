---
title: 界面概述
description: Obtainium 界面概述
---

# 界面概述 {#ui-overview}

屏幕底部的标签栏是查看 Obtainium 的主要方式。

## 应用列表 {#apps-page}

主屏包含 Obtainium 正在跟踪的应用列表，并提供每个应用的基本信息。

在此页面中，您可以使用屏幕底部的按钮同时对多个应用执行各种操作（如删除、更新、标记等）。选择一个或多个应用后，可以长按进入多选模式，也可以使用“全选”按钮。

您还可以按下“筛选”按钮来筛选特定的应用。这样就可以只查看符合特定条件（如已安装/未安装、最新/过期、源网站等）的应用。

## 添加应用到应用列表 {#add-app-page}

此页面可让您通过应用源链接添加应用。

当您输入应用源链接时，Obtainium 会自动检测应使用哪种[应用源](app_tracking.md/#basic)，并显示相关选项。如果链接与任何受支持的应用源不对应，则会默认选择“[HTML](sources.md/#html)”源。该应用源是一种通用的后备方案，在某些情况下可能有效。如果你认为 Obtainium 做了错误的选择，你可以手动指定要使用的源类型。

对于大多数应用源，输入的链接不需要太精确；例如，GitHub 源会接受任何包含基础仓库链接的 GitHub 链接（例如，`https://github.com/ImranR98/Obtainium/releases/latest` 会自动缩减为 `https://github.com/ImranR98/Obtainium` ）。不过，在两种情况下，您的链接必须更加精确：

1. 使用 HTML 源时
      - 例如，Tor Android APK 位于 `https://www.torproject.org/download/` ，因此只输入 `https://www.torproject.org/` 是不行的。
2. 手动选择应用源时（覆盖 Obtainium 的 HTML 回退选择）

此页面还可让您在支持此功能的源中搜索应用（[导入/导出](#importexport-page) 页面也提供了单独的搜索工具）。请注意，一个应用出现在搜索结果中并不意味着它将被成功添加，它还需要满足所有其它条件。

最后，该页面列出了所有支持的应用源，以及源是否可搜索等附加信息。

## 导入/导出 {#importexport-page}

通过此页面，您可以导出 Obtainium 数据，以便日后导入。您还可以启用自动导出功能，只要数据发生变化，就会自动导出。

此页面还提供了导入大量应用的各种其它方法，包括通过搜索。

本页的搜索工具还可让您搜索需要指定应用源服务器/域的源，例如[第三方 F-Droid 仓库](sources.md/#f-droid-third-party-repo)。

## 设置 {#settings-page}

该页面提供各种用户界面和行为设置，包括通过添加所需凭证为特定源启用更多功能的选项。有关具体设置的更多信息，请参阅[设置](settings.md)。
