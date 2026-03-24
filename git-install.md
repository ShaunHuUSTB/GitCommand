# 下载安装

1. Download
2. Install
3. 换行符转换
   - windows系统推荐默认：**Checkout as-is, commit Unix-style line endings**
     `git config --global core.autocrlf true`
   - macOS / Linux /windows->linux(C++)用户推荐: **Checkout Windows-style, commit Unix-style line endings**
     `git config --global core.autocrlf input`

# 基本配置

1. 设置用户名：`git config --global user.name "YourName"`
2. 设置邮箱：`git config --global user.email "your@email.com"`
3. 针对特定域名设置代理
   ```
   git config --global http.https://github.com.proxy http://username:password@127.0.0.1:7890
   git config --global http.https://github.com.sslVerify false
   git config --global https.https://github.com.proxy http://username:password@127.0.0.1:7890
   git config --global https.https://github.com.sslVerify false
   ```

# 配置SSH

1. 生成 RSA 密钥: `ssh-keygen -t rsa -C "your\_email@example.com"`
2. 拷贝公钥：`/c/Users/YourName/.ssh/id_public`
3. 代码仓库settings添加SSH Key

# TortoiseGit安装配置

1. 配置git: `C:\Program Files\Git\bin\git.exe`
2. 配置SSH 客户端：`C:\Program Files\Git\usr\bin\ssh.exe`
3. 配置diff工具：可默认或自选如beyond compare
