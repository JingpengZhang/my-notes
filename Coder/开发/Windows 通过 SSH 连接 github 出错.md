### 问题描述

在新 windows 电脑上安装开发环境，通过 `ssh keygen -t rsa` 生成公钥，并将公钥添加到 github 账户中，后，通过 `ssh -T github@github.com` 命令测试与 github 的连接时，报错 `ssh: connect to host github.com port 22: Connection timed out`。

### 解决方案

可能是网络供应商在出口防火墙上屏蔽了 22 端口，好在 github 运行使用 443 端口进行连接。

使用如下命令测试能否通过 443 端口连接 github 。

```bash
ssh -T -p 443 git@ssh.github.com
```

提示：
```bash
The authenticity of host '[ssh.github.com]:443 ([20.205.243.160]:443)' can't be established.
ECDSA key fingerprint is SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

输入 `yes` 后提示：

```bash
Warning: Permanently added '[ssh.github.com]:443,[20.205.243.160]:443' (ECDSA) to the list of known hosts.
Hi JingpengZhang! You've successfully authenticated, but GitHub does not provide shell access.
```

说明能够通过 443 端口连接 github，现在只需要设置 ssh 在连接 github 时默认通过 443 端口，就能正常使用 git 命令了。

在 `.ssh` 文件夹下新建 `config` 文件（如果有直接打开修改），在文件中添加如下代码：

```bash
Host github.com
 Hostname ssh.github.com
 Port 443
```

#### 测试

在终端运行

```bash
ssh -T git@github.com
```

出现

```bash
Hi JingpengZhang! You've successfully authenticated, but GitHub does not provide shell access.
```

即表示成功。