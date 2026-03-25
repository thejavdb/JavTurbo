# JavTurbo

语言 / Language: [English](./README.md)

JavTurbo 是一个桌面应用，用于扫描本地 JAV 视频、抓取元数据、下载资源，并将整理结果输出给 Jellyfin、Emby、Kodi、Plex 等媒体库工具使用。

## 功能特性

- 按扩展名和文件大小过滤，扫描本地媒体目录
- 自动从文件名解析 JAV 番号
- 并发刮削元数据——速度快于 mdcx、mdcng 和 metatube
- 支持 DMM/Fanza 和 MGS 的高清封面抓取，失败时自动回退至标准清晰度
- 刮削前自动检测重复番号，跳过重复影片避免冲突
- 可配置文件夹、文件名、NFO 标题命名模板
- 可下载资源：poster、thumb、fanart、trailer、NFO、extrafanart、behind-the-scenes
- 支持使用 `ffmpeg` 将 behind-the-scenes 转换为 MP4
- 刮削后清理：按扩展名或大小删除文件，删除空文件夹
- 实时进度条与结构化运行日志，每次刮削生成独立日志文件
- 控制台页面支持时间线视图、按影片分组、级别筛选和关键字搜索
- 多语言界面（`en`、`zh-CN`、`zh-TW`）

## 环境要求

- 可选：将 `ffmpeg` 加入 PATH——仅在需要 behind-the-scenes MP4 转换时使用

## 使用方法

### 1. 设置

打开 **设置** 进行配置：

- **媒体目录** — 存放视频文件的目录
- **成功输出目录** — 处理成功的视频和资源将移动到此处
- **失败输出目录** — 无法处理的视频将移动到此处
- **下载类型** — 选择需要下载的资源（poster、thumb、fanart、trailer、NFO、extrafanart、behind-the-scenes）
- **命名规则** — 文件夹模板、文件名模板、NFO 标题模板
- **并发数** — 并行下载和 ffmpeg 工作线程数量

### 2. 扫描

在主界面点击 **扫描**。JavTurbo 会遍历媒体目录，按扩展名和大小过滤，并从每个文件名解析番号。无法识别番号的文件将标记为失败。

### 3. 刮削

点击 **刮削** 处理所有待处理影片：

- 从 API 获取元数据
- 将视频移动并重命名至成功目录
- 写入 NFO
- 下载所选资源（poster、fanart、trailer 等）
- 如已配置，执行刮削后清理

刮削和扫描过程中，两个按钮均会禁用，防止重复操作。

### 4. 影片查看器

点击任意影片卡片打开查看器：

- 封面与元数据并排显示
- 简介显示在下方
- 预告片（显示封面缩略图与播放按钮）、正面封面和样本图片以网格展示
- 点击任意图片或预告片可打开全屏灯箱，使用左右按钮切换

### 5. 控制台

控制台页面实时展示所有刮削活动的日志。支持按级别筛选、关键字搜索、按影片分组。每次刮削还会在应用日志目录写入日志文件（`javturbo-scrape-YYYYMMDD-HHMMSS.log`）。

## 资源命名

为兼容 Jellyfin/Emby：

- 无前缀模式：
  - `poster.jpg`、`thumb.jpg`、`fanart.jpg`、`movie.nfo`、`trailer.mp4`
- 前缀模式：
  - `<视频文件名>-poster.jpg`、`<视频文件名>-thumb.jpg`、`<视频文件名>-fanart.jpg`、`<视频文件名>.nfo`、`<视频文件名>-trailer.mp4`

## License

当前仓库尚未包含明确的 License 文件。
