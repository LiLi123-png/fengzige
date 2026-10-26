---
name: submit-github
description: 提交当前项目到GitHub远程仓库并push。当用户要求提交到GitHub、上传到github仓库、或提到fengzige仓库时使用。不要用于Gitee或其他平台。
---

# Submit to GitHub

将当前工作区的改动通过 git commit 并 push 到指定的 GitHub 仓库。

## 目标仓库

- 远程仓库地址（SSH，公钥已配置）：`git@github.com:LiLi123-png/fengzige.git`
- 认证方式：SSH 公钥认证，无需令牌
- 远程名称使用 `github`，**不要占用 `origin`**（`origin` 已被 Gitee 仓库使用）

## 执行步骤

1. **检查 git 环境**
   - 确认当前目录是 git 仓库，若不是则执行 `git init`。
   - 检查 `git config user.name` 与 `user.email`，若未配置则设置本仓库级别身份（`user.name=feng-zige-123`，`user.email=fzg@example.com`），避免污染全局配置。

2. **验证 SSH 连接（可选但推荐）**
   - 执行 `ssh -T git@github.com`。
   - 输出包含 `successfully authenticated` 即为通过（退出码为 1 属正常现象）。
   - 若提示权限拒绝（Permission denied），说明公钥未生效，告知用户检查 `~/.ssh` 配置，不要改用令牌硬编码。

3. **暂存改动**
   - 执行 `git add -A` 暂存所有改动。
   - 运行 `git status --short` 确认暂存内容，向用户展示将提交的文件清单。

4. **提交**
   - 若用户未指定提交信息，使用带时间戳的默认信息，例如 `commit: 2026-10-26 10:00:00`。
   - 在 PowerShell 中使用单行 `-m` 参数传递提交信息，不要使用 bash heredoc 语法。
   - 执行 `git commit -m "<提交信息>"`。

5. **配置远程仓库**
   - 若不存在名为 `github` 的远程，添加：
     ```
     git remote add github git@github.com:LiLi123-png/fengzige.git
     ```
   - 若已存在 `github` 远程但 URL 不符，更新：
     ```
     git remote set-url github git@github.com:LiLi123-png/fengzige.git
     ```
   - 不修改 `origin`（Gitee）。

6. **推送**
   - 首次推送：`git push -u github <当前分支>`（当前分支一般为 `master`）。
   - 若远程仓库默认分支为 `main` 且为空仓库，可推送 `git push -u github master:main`。
   - 若推送被拒绝（远程有提交），先执行 `git pull github <分支> --rebase` 再推送，不要使用 `--force`。

7. **验证**
   - 执行 `git log -1 --oneline` 确认提交成功。
   - 执行 `git remote -v` 确认 `github` 远程指向正确且 `origin` 未被改动。
   - 执行 `git status` 确认工作区 clean、与上游同步。

## 注意事项

- 认证依赖 SSH 公钥，不要在命令、日志或提交信息中出现任何令牌或密码。
- 不要把 GitHub 凭据写入 `.git/config` 的 URL 中。
- 遇到 `Permission denied (publickey)` 时，指导用户运行 `ssh -T git@github.com` 排查，而非降级为 HTTPS 明文方案。
- 该 skill 与 `submit-project`（Gitee）互不影响：Gitee 用 `origin`，GitHub 用 `github`。
