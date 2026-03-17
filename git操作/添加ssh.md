### 第一步：检查并生成 SSH Key

打开你的 **Windows 终端** (PowerShell)，输入以下命令：

PowerShell

```
# 1. 检查是否已有密钥 (如果看到 id_rsa.pub 或 id_ed25519.pub 说明已有，跳到第三步)
ls ~/.ssh

# 2. 生成新密钥 (一路回车即可，不需要输入密码)
ssh-keygen -t ed25519 -C "你的GitHub邮箱"
```

------

### 第二步：将公钥添加到 GitHub

你需要把生成的“钥匙”告诉 GitHub：

1. **复制公钥内容**：在终端输入以下命令显示内容，然后完整复制出来（以 `ssh-ed25519` 开头的那一长串）：

   PowerShell

   ```
   cat ~/.ssh/id_ed25519.pub
   ```

2. **在 GitHub 设置**：

   - 登录 GitHub，点击右上角头像 -> **Settings**。
   - 左侧菜单找到 **SSH and GPG keys**。
   - 点击 **New SSH key**。
   - **Title** 随便起个名字（比如 `My-Laptop`），**Key** 粘贴刚才复制的内容。
   - 点击 **Add SSH key**。

------

### 第三步：修改本地仓库的远程地址

因为你之前的仓库是用 HTTPS 关联的，现在要把它改成 SSH 格式：

PowerShell

```
# 1. 先删掉旧的 HTTPS 地址
git remote remove origin

# 2. 添加 SSH 格式的地址 (注意格式是 git@github.com:...)
git remote add origin git@github.com:twistmh/my-notes.git

# 3. 验证一下
git remote -v
```

**现在的预期输出：**

> `origin  git@github.com:twistmh/my-notes.git (fetch)` `origin  git@github.com:twistmh/my-notes.git (push)`

------

### 第四步：测试并推送

1. **测试连接**：

   PowerShell

   ```
   ssh -T git@github.com
   ```

   *如果提示 `Are you sure you want to continue connecting?`，输入 **`yes`** 并回车。* *看到 `Hi twistmh! You've successfully authenticated...` 就说明彻底通了。*

2. **正式推送**：

   PowerShell

   ```
   git push -u origin master
   ```