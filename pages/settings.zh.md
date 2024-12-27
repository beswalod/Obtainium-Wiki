---
title: 设置
description: 对 Obtainium 设置项的说明
---

# 设置 {#settings}

对 Obtainium 设置项的说明

## 具体来源 {#source-specific}

GitHub 对特定时间内的 API 请求数量设置了上限。由于 Obtainium 使用 GitHub API 获取发行信息，因此如果你有几十个以上的来自 GitHub 源的应用，就可能会遇到“速率限制”错误。你可以通过获取个人访问令牌来解决这个问题。

GitLab 发行版有时会包含以非标准方式附加的 APK，因此 Obtainium 无法轻松获取它们。GitLab API 提供了更可靠的提取 APK 的方式，但没有 API 密钥就无法使用。虽然这对大多数 GitLab 仓库来说都不是问题，但您可以在 Obtainium 的设置中添加自己的个人访问令牌，以便在极端情况下更可靠地提取 APK。

### 设置个人访问令牌 {#setting-up-personal-access-tokens}

=== ":simple-github: GitHub"
    跟踪来自 GitHub 源的应用时避免 API 速率限制：

    1. 登录 [GitHub](https://github.com)。
    2. 进入开发者设置中的 [Fine-grained tokens](https://github.com/settings/tokens?type=beta) 部分。
    3. 选择 **Generate new token**。
    4. 给 Token 命名并设置有效期。
    5. 滚动到底部，选择 **Generate token**。
    6. 复制 Token 并将其粘贴到 Obtainium 设置中。请立即复制您的 Token，因为您将无法再次查看。

=== ":simple-gitlab: GitLab"
    更可靠地从来自 GitLab 源的发行版中提取 APK：

    1. 登录 [GitLab](https://gitlab.com)。
    2. 进入设置中的[个人访问令牌](https://gitlab.com/-/user_settings/personal_access_tokens)部分。
    3. 选择**添加新令牌**。
    4. 给令牌命名并设置有效期。
    5. 勾选“read_api”。
    6. 滚动到底部，选择**创建个人访问令牌**。
    7. 复制令牌并将其粘贴到 Obtainium 设置中。请立即复制您的令牌，因为您将无法再次查看。

    !!! info "何时需要这样做？"
        请参阅[该解释](https://github.com/ImranR98/Obtainium/issues/3#issuecomment-1234695412)，了解 GitLab 发行版中的非标准 APK 附件
