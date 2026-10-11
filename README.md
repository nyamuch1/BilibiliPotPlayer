# BilibiliPotPlayer

适用于 PotPlayer 的 Bilibili 插件。如果配合[油猴脚本](https://greasyfork.org/zh-CN/scripts/461800-bilibilipotplayer)，可以直接在网页打开 PotPlayer 进行播放

## 安装插件

[下载项目](https://github.com/chen310/BilibiliPotPlayer/archive/refs/heads/master.zip)

将项目 `Media/PlayParse` 路径下的 `MediaPlayParse - Bilibili.as`、`MediaPlayParse - Bilibili.ico` 和 `Bilibili_Config.json` 三个文件复制到 `{PotPlayer 安装路径}\Extension\Media\PlayParse` 文件夹下。

`MediaPlayParse - Bilibili.as` 提供了解析 `Bilibili` 链接的功能。

将项目 `Media/UrlList` 路径下的 `MediaUrlList - Bilibili.as` 和 `MediaUrlList - Bilibili.ico` 两个文件复制到 `{PotPlayer 安装路径}\Extension\Media\UrlList` 文件夹下。

`MediaUrlList - Bilibili.as` 提供了列出 `Bilibili` 常用链接的功能，使用方式为按下 <kbd>ctrl</kbd> + <kbd>U</kbd> 并选择要播放的项目，如下图所示

![UrlList](https://cdn.jsdelivr.net/gh/chen310/BilibiliPotPlayer/public/urllist.png)

## 登录

找到刚刚复制过去的配置文件 `Bilibili_Config.json`，填写 Cookie 等设置内容。 打开 PotPlayer，按 <kbd>F5</kbd> 打开选项，点击`扩展功能`下的`媒体播放列表/项目`，再点击 `Bilibili`，然后打开`账户设置`，填写配置文件路径，如 `D:\DAUM\PotPlayer\Extension\Media\PlayParse\Bilibili_Config.json`。每次修改完配置文件，可能都要重启 PotPlayer 才能生效。

![Settings](https://cdn.jsdelivr.net/gh/chen310/BilibiliPotPlayer/public/settings.png)

点击测试按钮，如果弹出账号信息，就说明登录成功。

![Test](https://cdn.jsdelivr.net/gh/chen310/BilibiliPotPlayer/public/test.png)

### Cookies 获取

[获取Cookie](https://github.com/chen310/BilibiliPotPlayer/issues/62#issuecomment-1841909583)

## 使用方法

### 播放视频/直播

将 Bilibili 链接拖到 PotPlayer，或者按 <kbd>ctrl</kbd> + <kbd>U</kbd> 粘贴 Bilibili 链接即可播放。可参考[视频](https://www.bilibili.com/video/BV1mM41177kT)

### 搜索

按 <kbd>ctrl</kbd> + <kbd>U</kbd>，在文件地址列表中选择`搜索`，然后到上面的输入框中替换关键词，最后回车即可

![Search](https://cdn.jsdelivr.net/gh/chen310/BilibiliPotPlayer/public/search.png)

### 跳过片头片尾

对于一些电视剧、番剧，能够跳过片头和片尾。具体设置为：在 PotPlayer 上点击鼠标右键，选择`播放`-`跳略播放`-`跳略播放设置`

![Skip_Settings](https://cdn.jsdelivr.net/gh/chen310/BilibiliPotPlayer/public/skip_1.png)

勾选`跳略播放`和`章节名称`，并在名称列表中追加`哔哩哔哩-片头`和`哔哩哔哩-片尾`两项，每一项之间用英文分号`;`隔开。

![Skip_Settings](https://cdn.jsdelivr.net/gh/chen310/BilibiliPotPlayer/public/skip_2.png)

### 在列表中显示缩略图

按 <kbd>F6</kbd> 打开播放列表，点击鼠标右键，点击`样式`，选择`显示缩略图`，即可显示视频的缩略图。

![Thumbnail](https://cdn.jsdelivr.net/gh/chen310/BilibiliPotPlayer/public/thumbnail.png)

### 创建自动更新的播放列表

按 <kbd>F6</kbd> 打开播放列表，点击新建专辑，起一个合适的专辑名称，选择外部播放列表，并填写相应的链接，再点击确定即可。这样就得到一个可以自动更新的列表。

![Create_Playlist](https://cdn.jsdelivr.net/gh/chen310/BilibiliPotPlayer/public/create_playlist_1.png)

![Create_Playlist](https://cdn.jsdelivr.net/gh/chen310/BilibiliPotPlayer/public/create_playlist_2.png)

### 播放分享短链

B 站 App 的「分享」复制出来的 `https://b23.tv/xxxxx` 短链可以直接拖进 PotPlayer 播放。

## 关于画质

- **默认地址就是最高画质那一档**，走 DASH。同一个清晰度有多个编码时优先 AVC，兼容性最好。
  实测：普通视频默认 `1080P+ AVC 1920x1080 5.25Mbps`，4K 视频默认 `4K 超清 AVC 3840x2160 8.35Mbps`。
- **DASH 的视频轨和音频轨是分开的**，所以默认打开只有画面。想要声音有两个办法：
  - 在清晰度菜单里选 `★ xxx 音视频合一` 那一条 —— 这是插件额外附上的一路 mp4，
    画面+声音一次到位（清晰度是 B 站 mp4 模式的上限，比 `dash` 低一档）。
  - 或者选一条 `AAC ...` 音轨条目。菜单里的每一档都是独立的可选流，
    PotPlayer 不一定会把它和当前的视频轨合起来播，所以推荐上一条。
- 说明：PotPlayer 本身支持"视频 + 单独音轨一起播"（右键 → 打开 → 载入音频，或者命令行
  `/same` 一次加载多条流），但这两种方式都没法由扩展脚本触发 —— `PlayParse` 的选区列表
  只能提供一串互相替代的流，不能给视频挂一条独立音轨。
- 菜单里的每一档都实测过，分辨率/编码和标签一致（比如 `4K 超清 AVC` 实测就是 `3840x2160 avc1`）。
- **未登录时 B 站只提供到 480P**（`dash` 里只有 480P/360P 两档），这是服务端限制，不是插件的问题。
  1080P/4K 需要配置 Cookie；4K 及以上还需要大会员。
- 直播清晰度取的是 `getRoomPlayInfo` 返回的当前清晰度。菜单里显示的就是服务端**实际返回**的档位：
  未登录最高「超清」，登录后是「原画」（实测 1920x1080 60fps 约 2.8Mbps），
  服务端把多档压成同一路时会自动去重。
- CDN 域名带 `.mcdn.bilivideo.cn`（B 站的 P2P 节点）时容易 503 或速度慢，
  插件会自动改用 `backupUrl` 里的普通节点。

## 弹幕与字幕

**不再需要任何第三方服务器。**

- **弹幕**：插件直接取 `https://comment.bilibili.com/<cid>.xml`，自己转成 ASS 交给
  PotPlayer 当字幕渲染（滚动弹幕用 `\move` 分轨道排列，顶部/底部弹幕用 `\pos` 固定）。
  原来那个弹幕服务器 `subtitle.chen310.repl.co` 已随 `repl.co` 域名下线，现在用不上了。
- **字幕**：直接用 B 站自己的字幕地址（`//aisubtitle.hdslb.com/...`）。这也是 issue
  [#157](https://github.com/chen310/BilibiliPotPlayer/issues/157) 里作者确认过的 ——
  可以直接把 JSON 格式的字幕 url 交给 PotPlayer，也可以用 `fileContent` 直接塞文本。

想改回自建服务器的话，`Bilibili_Config.json` 里填 `danmaku.server` 即可，插件会优先走服务器。

> 弹幕渲染依赖 PotPlayer 支持 `fileContent` / JSON 字幕，这个能力大约 2025 年初之后的版本才有。

## 已知失效的功能

以下功能依赖 B 站已经下线的接口，无法通过改插件恢复：

- **音频区（`www.bilibili.com/audio/au...`、`am...`）**：B 站已下线音频区，接口固定返回
  `4511001 音频未找到或已下架`。

## 更新记录

- 适配 B 站改版后的接口：排行榜改用页面 Referer 过风控、分区最新改用 `newlist`、
  直播间信息与推流改用 `getRoomPlayInfo` / `getRoomBaseInfo`、直播分区列表改用 `getRoomList`。
- 修复直播推流地址降级：旧接口 `playUrl/playUrl` 无论 `qn` 传什么最高只给「高清」，
  新接口可以拿到「原画」（实测旧接口 854x480 699kbps → 新接口 1920x1080 60fps 2.8Mbps）。
- 修复默认画质错误：原先循环里 `url` 被反复覆盖，最后返回的是清晰度**最低**的一路；
  现在固定取最高的一路。
- **修复「视频信息能显示、视频却无法播放」**：B 站的 CDN 对取流请求同时校验
  User-Agent **和** Referer，少一个都返回 403，而 PotPlayer 取流时什么都不带，
  所以 `OnInitialize()` 里两个头都补上了。
  元数据和缩略图走 `api.bilibili.com`，不受影响，所以症状表现为「信息有、画面没有」。
- **补上漏掉的 CDN 域名 `mountaintoys.cn`**：`HostSetUrlHeaderHTTP` 只对**注册过的域名**
  生效，没注册的一律不带请求头。B 站现在会有一部分地址落在
  `*.edge.mountaintoys.cn` 上（实测 140 个视频里占 122 次），这类视频以前必定 403。
  `preferCdn()` 现在也会避开未注册域名。
- 支持 `b23.tv` 分享短链。
- 直播优先 HLS 而不是 FLV：HLS 时间轴连续，PotPlayer 断线重连后不会出现声音重复/回声。
- 弹幕和字幕不再依赖第三方服务器（原来内置的 `subtitle.chen310.repl.co` 已下线）：
  弹幕直接由 `comment.bilibili.com/<cid>.xml` 转 ASS，字幕直接用 B 站自己的 JSON 地址。
- 未读到 cookie 时在控制台给出明确提示。
