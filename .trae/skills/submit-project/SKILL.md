---
name: submit-project
description: 提交当前项目到Gitee远程仓库，执行git add、commit并push。当用户要求提交项目、上传代码、git commit并push、或推送到Gitee时使用。不要用于其他代码托管平台。
---

# Submit Project

将当前工作区的改动通过 git commit 并 push 到指定的 Gitee 仓库。

## 目标仓库

- 远程仓库地址：`https://gitee.com/feng-zige-123/fzg.git`
- 认证方式：使用私人令牌（Personal Access Token）作为密码

令牌存储在同目录下的 `secret.env` 文件中，文件内容格式为 `GITEE_TOKEN=<令牌值>`。执行前先读取该文件获取令牌。**切勿将令牌硬编码或输出到日志/提交信息中。**

## 执行步骤

1. **检查 git 环境**
   - 确认当前目录是 git 仓库，若不是则执行 `git init`。
   - 检查 `git config user.name` 与 `user.email`，若未配置则设置本仓库级别身份（例如 `user.name=feng-zige-123`，`user.email=fzg@example.com`），避免污染全局配置。

2. **暂存改动**
   - 执行 `git add -A` 暂存所有改动。
   - 运行 `git status` 确认暂存内容。

3. **提交**
   - 若用户未指定提交信息，使用带时间戳的默认信息，例如 `commit: 2026-10-15 14:30:00`。
   - 在 PowerShell 中使用单行 `-m` 参数传递提交信息，不要使用 bash heredoc 语法。
   - 执行 `git commit -m "<提交信息>"`。

4. **配置远程仓库**
   - 若不存在 `origin` 远程，添加：
     ```
     git remote add origin https://gitee.com/feng-zige-123/fzg.git
     ```
   - 若已存在 `origin`，更新其 URL 为上述地址。
   - 使用带令牌的 URL 推送：`https://oauth2:<令牌>@gitee.com/feng-zige-123/fzg.git`
     - 注意：推送完成后应将远程 URL 还原为不含令牌的普通地址，避免令牌长期保存在 `.git/config` 中。

5. **推送**
   - 执行 `git push -u origin <当前分支>`（首次推送加 `-u` 设置上游）。
   - 若本地分支为 `master` 而远程默认分支为 `main`，使用 `git push origin master:main`。

6. **验证**
   - 执行 `git log -1` 确认提交成功。
   - 执行 `git remote -v` 确认远程 URL 已还原为不含令牌的地址。

## 注意事项

- `secret.env` 已在 `.gitignore` 中忽略，不会被提交。
- 不要将令牌写入提交信息、代码或日志。
- 遇到认证失败时，检查令牌是否过期或权限不足。
