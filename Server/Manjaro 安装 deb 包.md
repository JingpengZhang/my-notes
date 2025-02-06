#### 1. 安装 `debtap`
```shell
yay -S debtap
```

#### 2. 将 `deb`包转换为 `arch` 包
```shell
debtap -q xxx.deb
```

#### 3. 使用 `pacman` 安装
```shell
sudo pacman -U xxx.pkg.tar.zst
```
