# Git 本地配置：同时使用 GitHub 和 Gitee，并保护邮箱隐私

本文适用于 macOS、Linux、Windows（Git Bash）。目标是：

- GitHub 提交使用 GitHub 提供的 `noreply` 邮箱。
- Gitee 提交使用 Gitee 提供的“不公开邮箱”。
- 不把真实个人邮箱写进新提交。
- 同一台电脑可以同时维护 GitHub 和 Gitee 仓库，不必每次手动切换邮箱。

> **关键点：** GitHub 和 Gitee 的隐私邮箱通常不同，不能把一个平台的 noreply 邮箱当作另一个平台的邮箱使用。建议按本地仓库目录自动选择对应邮箱。

## 1. 在平台获取隐私邮箱

### GitHub

1. 打开 [GitHub 邮箱设置](https://github.com/settings/emails)。
2. 开启 **Keep my email addresses private**（保持我的邮箱地址私有）。
3. 建议同时开启 **Block command line pushes that expose my email**（阻止命令行推送暴露个人邮箱）。
4. 复制页面显示的完整 GitHub-provided `noreply` 邮箱。不要猜格式，通常类似 `数字ID+用户名@users.noreply.github.com`。

官方说明：[设置提交邮箱](https://docs.github.com/en/account-and-profile/how-tos/email-preferences/setting-your-commit-email-address)。

### Gitee

1. 打开 [Gitee 邮箱管理](https://gitee.com/profile/emails)。
2. 找到“不公开邮箱”相关设置并启用。
3. 复制页面显示的完整不公开邮箱，通常为 `数字ID+用户名@user.noreply.gitee.com` 一类格式。以账号页面实际显示为准。
4. 如果页面提供“提交邮箱”设置，确认使用该不公开邮箱。

Gitee 的设置名称或页面布局可能变化，请以当前账号页面为准。官方帮助：[提交第一行代码](https://gitee.com/help/articles/4122)。

## 2. 推荐方案：按仓库目录自动选择邮箱

把 GitHub 仓库统一放在 `~/code/github/`，把 Gitee 仓库统一放在 `~/code/gitee/`。Git 会根据仓库所在目录自动加载对应的提交邮箱配置。

### 第一步：设置全局用户名和安全兜底

将名字替换成你希望显示在提交记录中的昵称：

```bash
git config --global user.name "你的昵称"
git config --global user.useConfigOnly true
```

`user.useConfigOnly true` 会避免 Git 在未明确配置提交身份时自动猜测身份。下面会为两个平台分别设置邮箱。

### 第二步：创建 GitHub 专用配置

将命令里的邮箱替换成你从 GitHub 设置页面复制的完整 noreply 地址：

```bash
git config --file ~/.gitconfig-github user.name "你的昵称"
git config --file ~/.gitconfig-github user.email "你的-GitHub-noreply-邮箱"
```

### 第三步：创建 Gitee 专用配置

将邮箱替换成 Gitee 设置页面显示的完整不公开邮箱：

```bash
git config --file ~/.gitconfig-gitee user.name "你的昵称"
git config --file ~/.gitconfig-gitee user.email "你的-Gitee-noreply-邮箱"
```

### 第四步：让 Git 根据目录加载配置

打开用户主目录下的 `.gitconfig` 文件，在文件末尾添加以下内容。不要覆盖文件里已有的其他配置：

```ini
[includeIf "gitdir:~/code/github/"]
    path = ~/.gitconfig-github

[includeIf "gitdir:~/code/gitee/"]
    path = ~/.gitconfig-gitee
```

如果没有该文件，可以先运行 `git config --global --list --show-origin` 查看全局配置位置；通常是用户主目录中的 `.gitconfig`。

**目录规则：**

- GitHub 仓库放在 `~/code/github/仓库名`。
- Gitee 仓库放在 `~/code/gitee/仓库名`。
- 路径匹配对仓库目录生效，建议保持末尾的斜杠。
- 如果你把仓库放在其他目录，按实际路径修改 `.gitconfig` 的规则。

例如，克隆仓库：

```bash
mkdir -p ~/code/github ~/code/gitee
git clone git@github.com:用户名/仓库名.git ~/code/github/仓库名
git clone git@gitee.com:用户名/仓库名.git ~/code/gitee/仓库名
```

如果使用 HTTPS 地址，把上面的 SSH 地址替换为平台提供的 HTTPS 克隆地址即可。邮箱配置与 HTTPS/SSH 认证方式无关。

## 3. 验证配置是否生效

分别进入一个 GitHub 仓库和一个 Gitee 仓库，执行：

```bash
git config --show-origin --get user.email
git var GIT_AUTHOR_IDENT
git var GIT_COMMITTER_IDENT
```

检查输出中的邮箱：

- GitHub 仓库应显示 GitHub 的 `noreply` 邮箱。
- Gitee 仓库应显示 Gitee 的不公开邮箱。
- 如果输出真实个人邮箱，先不要提交；检查仓库级配置和 `.gitconfig` 的目录匹配。

查看某项配置来自哪里：

```bash
git config --show-origin --get user.email
git config --show-origin --get-regexp '^includeIf\\.'
```

## 4. 已有仓库的处理

如果仓库不在上面约定的目录中，最简单的做法是在仓库目录内单独设置邮箱：

GitHub 仓库：

```bash
git config --local user.email "你的-GitHub-noreply-邮箱"
```

Gitee 仓库：

```bash
git config --local user.email "你的-Gitee-noreply-邮箱"
```

仓库级的 `user.email` 会覆盖全局或条件加载的邮箱。若曾设置过错误的仓库级邮箱，可以在该仓库执行 `git config --local --unset user.email`，然后重新验证条件配置是否生效。

## 5. 注意：隐私邮箱不会修复历史提交

修改 Git 配置只影响之后创建的提交，不会改写过去的提交。查看当前分支的提交邮箱：

```bash
git log -10 --format="%h %an <%ae> | %cn <%ce>"
```

如果历史中出现真实邮箱，先评估是否需要重写提交历史。重写历史会改变提交 SHA，且无法保证已经被他人复制或缓存的旧记录消失。

另外，邮箱隐私只保护 Git 提交中的邮箱字段；提交作者名称、代码内容、仓库地址、提交时间等信息仍可能公开。不要把密码、令牌、私钥或含有秘密的配置文件提交到仓库。
