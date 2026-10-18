# sys-toolkit

系统管理和网络工具脚本集合，支持 Linux 和 macOS。

## 目录

- [网络代理 (Sing-box / Snell)](#网络代理-sing-box--snell)
- [系统备份恢复 (rclone)](#系统备份恢复-rclone)
- [fail2ban 管理](#fail2ban-管理)
- [Docker 安装](#docker-安装)
- [图床工具 (img)](#图床工具-img)

## 网络代理 (Sing-box)

Sing-box（Snell / Shadowsocks2022 / VLESS+Reality / Hysteria2 / AnyTLS / SOCKS5 / HTTP）的安装、配置、节点管理与中转。其中 Snell 节点类型自 sing-box 1.14.0 起支持。

```bash
curl -fsSL https://raw.githubusercontent.com/mlang233/sys-toolkit/master/server-proxy.sh -o server-proxy.sh
chmod +x server-proxy.sh
sudo ./server-proxy.sh
```

要求：Linux（systemd），root 权限；Sing-box 使用官方通用安装器（deb/rpm、Arch Linux 等）。安装时可选择正式版 / 最新 Beta 版 / 指定版本，其中 Snell 节点需 sing-box ≥ 1.14.0（当前最新正式版 v1.13.19 不支持，需选择 Beta 版）。

## 系统备份恢复 (rclone)

基于 rclone 的系统备份与恢复，支持 S3 / Cloudflare R2 / 阿里云 OSS / 腾讯云 COS 等云存储。

```bash
curl -fsSL https://raw.githubusercontent.com/mlang233/sys-toolkit/master/sys-backup-restore.sh -o sys-backup-restore.sh
chmod +x sys-backup-restore.sh
sudo ./sys-backup-restore.sh
```

要求：Linux（systemd），root 权限。

## fail2ban 管理

fail2ban 入侵检测和防护的安装、配置、Jail 与 IP 管理。安装时自动检测 SSH 监听端口、journald/传统日志文件以及活动的 UFW，兼容 Debian 13 等默认不安装 `sudo`、不生成 `/var/log/auth.log` 的精简系统。

```bash
curl -fsSL https://raw.githubusercontent.com/mlang233/sys-toolkit/master/fail2ban-manager.sh -o fail2ban-manager.sh
chmod +x fail2ban-manager.sh
sudo ./fail2ban-manager.sh
```

要求：Linux（systemd），root 权限；支持 apt/dnf/yum/pacman/zypper（发行版软件源需提供 fail2ban）。

## Docker 安装

Docker 与 Docker Compose 一键安装，支持国内镜像源（阿里云 / 清华 TUNA）。

```bash
curl -fsSL https://raw.githubusercontent.com/mlang233/sys-toolkit/master/docker-install.sh -o docker-install.sh
chmod +x docker-install.sh
sudo ./docker-install.sh
```

要求：Linux（Ubuntu/Debian/CentOS/RHEL/Rocky/Alma/Fedora），root 权限。

## 图床工具 (img)

通用 S3 / Cloudflare R2 图床工具箱，支持上传、剪贴板粘贴、删除，也可作为 Typora 自定义上传器。

```bash
curl -fsSL https://raw.githubusercontent.com/mlang233/sys-toolkit/master/img.sh -o img.sh
chmod +x img.sh

# 方式一：直接执行（Typora 兼容）
./img.sh cat.png

# 方式二：source 后使用 img 子命令（交互更友好）
source img.sh
img setup               # 引导式初始化配置
img up    cat.png       # 上传文件 → 输出公开 URL
img pup                 # 上传剪贴板图片 (macOS)
img rm    <url|key>     # 删除远程图片
img uninstall           # 彻底卸载
```

要求：macOS，Homebrew（用于自动安装 AWS CLI），S3 兼容存储（Cloudflare R2 / AWS S3 等）。
