---
title: Hello SketchyBar
author: MrKeanu
categories:
  - Incessant Coding-编程不辍
  - Hello World
index_img: /image/index/skybar.png
banner_img: /image/bg/cat_with_fish.jpg
banner_img_height: 70
banner_mask_alpha: 0.3
date: 2026-10-19 01:54:36
subtitle:  高度客制化，不得不摸索的效率工具之一
excerpt: 替代macOS原生状态栏，打造个人高效工作流。
tags:
archive:
hide:
math: true
mermaid: true
---


## Introduce
SketchyBar是macOS顶部菜单栏（status bar）的替代品，与2021年由**FelixKratz**用Swift/AppleKit写成，本质是一个无边框窗口，可以像“容器”一样插入**item**。SketchyBar提供了高度的客制化潜力，用来打造一个个人自用的“提效”状态栏非常合适。

SketchyBar 示例如下：
![SketchyBar Examples](https://felixkratz.github.io/SketchyBar/assets/images/examples-e91544141827cce7e424ef77f613cea2.png)
总体而言SketchyBar可玩性非常高，上手也不算难。而且在社区[^1]中有更多网友制作的有趣且美观的SketchyBar可供参考。

目前SketchyBar常见的组织形式为：
```
- .config/
  - sketchybar/
    - items/          # 集成后的单个元素
    - plugins/        # 存放素有回脚本
      sketchybarrc    # 配置文件
```
其中`sketchybarrc`为实际的配置文件，当启动SketchyBar时会自动执行该脚本，这就类似`.zshrc`一般。

### Bar
整个顶部区域都可称之为 **Bar**，其全局属性用 `--bar` 设置：

```bash
sketchybar --bar position=top height=32 margin=0 \
                 color=0xcc1e1e2e blur_radius=20 \
                 padding_left=8 padding_right=8
```

默认 `display=all`，即**每个显示器各画一条**，共用同一份配置；也可以只显示在主屏：

```bash
sketchybar --bar display=main
```

常用 bar 属性：

|属性|说明|默认|
|---|---|---|
|`position`|`top` / `bottom`|`top`|
|`height`|高度（点）|`25`|
|`margin`|四周外边距|`0`|
|`y_offset`|垂直偏移|`0`|
|`corner_radius`|圆角|`0`|
|`border_width` / `border_color`|边框|`0` / 红|
|`blur_radius`|背景模糊|`0`|
|`padding_left` / `padding_right`|左右内边距|`0`|
|`notch_width` / `notch_offset` / `notch_display_height`|刘海相关|`200` / `0` / `0`|
|`display`|`main` / `all` / 显示器编号列表|`all`|
|`hidden`|`off` / `on` / `current`|`off`|
|`topmost`|是否盖住所有窗口|`off`|
|`sticky`|space 切换时是否保持|`on`|
|`shadow`|是否画阴影|`off`|
|`font_smoothing`|字体平滑|`off`|

### Item

bar 里最小的可配置单元。一个 item 可以同时拥有：

- 一个 **icon**
- 一个 **label**
- 一个 **background**
- 一张 **image**
- 一个 **popup**
- 一组 **script**

添加语法：

```bash
sketchybar --add item <名字> <位置>
```

位置只能是：

|位置|含义|
|---|---|
|`left`|左区|
|`right`|右区|
|`center`|中区|
|`q`|刘海左侧（notch 左）|
|`e`|刘海右侧（notch 右）|

关键规则：**同一区域内的显示顺序 = `--add` 的先后顺序**。后加的排在后面，可以用 `--move` / `--reorder` 调整。

item 还可以绑定到特定 space / display：

```bash
sketchybar --set <名字> space=1 display=2
```

这样它只在“第 1 个 space、第 2 块屏”出现。`ignore_association=on` 可以临时忽略这些绑定。

### Component

组件本质上是“带额外能力的 item”，普通 item 的属性它全都有。

| 组件        | 添加语法                         | 额外能力                    |
| --------- | ---------------------------- | ----------------------- |
| `space`   | `--add space space.1 left`   | 代表一个 Mission Control 桌面 |
| `bracket` | `--add bracket <名> <成员...>`  | 把多个 item 包在同一个背景里       |
| `graph`   | `--add graph <名> <位置> <宽度>`  | 画折线图                    |
| `slider`  | `--add slider <名> <位置> <宽度>` | 可点击/拖动的进度条              |
| `alias`   | `--add alias <App名> <位置>`    | 镜像 macOS 原生菜单栏图标        |

### Popup

每个 item 天生带一个 popup 容器。把子 item 的位置写成 `popup.<父名字>` 就挂进去了：

```bash
sketchybar --add item apple.about popup.apple.logo
```

父 item 点击时切换显示：

```bash
sketchybar --set apple.logo click_script="sketchybar --set apple.logo popup.drawing=toggle"
```

popup 属性：

|属性|说明|默认|
|---|---|---|
|`popup.drawing`|开/关|`off`|
|`popup.horizontal`|横向排列|`off`|
|`popup.topmost`|是否最顶层|`on`|
|`popup.height`|**行与行之间的间距**（不是总高度）|bar 高度|
|`popup.y_offset`|垂直偏移|`0`|
|`popup.align`|`left` / `right` / `center`|`left`|
|`popup.blur_radius`|背景模糊|`0`|
|`popup.background.*`|背景属性|—|

### Event + Script

item 可以订阅事件；事件发生时执行它的 `script`：

```bash
sketchybar --subscribe <名字> <事件> [<事件>...]
```

脚本里可用的环境变量：

|变量|含义|
|---|---|
|`$NAME`|触发脚本的 item 名字|
|`$SENDER`|事件名（定时触发时是 `routine`）|
|`$INFO`|事件附带的额外信息（JSON/字符串）|
|`$CONFIG_DIR`|配置文件所在目录|
|`$BUTTON`|点击键：`left` / `right` / `other`|
|`$MODIFIER`|`shift` / `ctrl` / `alt` / `cmd`|
|`$SCROLL_DELTA`|滚轮增量|
|`$SELECTED` / `$SID` / `$DID`|仅 space 组件|

**Script vs click_script**

| 属性              | 何时执行                                      |
| --------------- | ----------------------------------------- |
| `script=`       | 订阅的事件触发时、`update_freq` 定时到点时、`--update` 时 |
| `click_script=` | 内联写鼠标点击时执行的脚本                             |

如果点击逻辑需要知道 `$BUTTON` / `$MODIFIER`，就用 `--subscribe <名> mouse.clicked` 配 `script`；`click_script` 适合“点一下就跑”的简单场景。

### Config
SketchyBar配置文件的默认路径为：

``` shell
~/.config/sketchybar/sketchybarrc
```

配置文件其实是一个`shell`脚本，本质上就是一串SketchyBar指令发送可后台守护进程执行。

## Quick Start
标准启动流程如下：

``` shell
brew services start sketchybar    # 开机自启 + 后台运行
sketchybar                        # 前台运行，能看到所有脚本报错
sketchybar --reload               # 重载当前配置（效果等同重启进程）
sketchybar --reload /path/to/rc   # 换一份配置
sketchybar --config /path/to/rc   # 启动时指定配置
sketchybar --hotload true         # 监视配置目录，改文件自动重载
```


## Commands
以下就是 `sketchybar --help` 的全部命令，按用途分组。

### 启动 / 全局

|命令|作用|
|---|---|
|`sketchybar -c, --config <file>`|指定配置文件启动|
|`sketchybar --bar k=v ...`|设置全局 bar 属性|
|`sketchybar --default k=v ...`|修改“之后新建 item”的默认属性|
|`sketchybar --hotload true\|false`|开关配置热重载|
|`sketchybar --reload [path]`|重载配置|
|`sketchybar --update`|强制所有脚本跑一遍、所有事件重发一次|
|`sketchybar --load-font <path>`|从任意路径加载字体文件|

> `--update` 一般放在 `sketchybarrc` 最后一行，用来初始化那些“只在事件里更新”的 item。**绝不要把它写进 item 的脚本里**，否则无限递归。

### 增删改 item

|命令|作用|
|---|---|
|`--add item <名> <位置>`|新建 item|
|`--set <名> k=v ...`|修改属性；名字支持 `/正则/`|
|`--remove <名>`|删除 item，支持 `/正则/`|
|`--rename <旧> <新>`|改名|
|`--clone <父> <新> [before\|after]`|克隆一个 item|
|`--move <名> before\|after <参照>`|移动到参照物前/后|
|`--reorder <名> <名> ...`|按给定顺序重排这些 item|
|`--default k=v ...`|改默认值，只影响之后创建的 item|

`--set` 的正则示例（注意 shell 引号，避免被当成 glob）：

```bash
sketchybar --set '/space\..*/' label.drawing=off
sketchybar --remove '/temp\..*/'
```

### 组件

|命令|作用|
|---|---|
|`--add space <名> <位置>`|新建 space 组件|
|`--add bracket <名> <成员...>`|新建 bracket，成员可用 `/正则/`|
|`--add graph <名> <位置> <宽度>`|新建 graph|
|`--push <名> <0~1 的数值...>`|往 graph 推数据点|
|`--add slider <名> <位置> <宽度>`|新建 slider|
|`--add alias <App名> <位置>`|镜像原生菜单栏项|

### 事件

|命令|作用|
|---|---|
|`--subscribe <名> <事件> ...`|订阅事件|
|`--add event <名> [NSDistributedNotification名]`|自定义事件（可桥接系统/App 通知）|
|`--trigger <事件> [VAR=值 ...]`|手动触发事件，并可传环境变量|

### 查询（debug）

|命令|输出|
|---|---|
|`--query bar`|bar 的全部属性（JSON）|
|`--query <名>`|某个 item 的全部属性（JSON）|
|`--query defaults`|当前默认属性|
|`--query events`|已注册事件|
|`--query default_menu_items`|可被 alias 的原生菜单栏项|
|`--query displays`|显示器信息|

```bash
sketchybar --query clock | jq
```

属性名拼错时 SketchyBar **不会报错，只会静默忽略**，所以“设了没反应”时第一件事就是 `--query` 看值到底有没有进去。

### 动画

```bash
sketchybar --animate <曲线> <时长> \
           --bar k=v ... \
           --set <名> k=v ...
```

曲线：`linear`、`quadratic`、`tanh`、`sin`、`exp`、`circ`。

时长单位是**帧数（按 60Hz 计）**，所以 `30` ≈ 0.5 秒。可以链式写多个同名属性做关键帧：

```bash
sketchybar --animate sin 20 --set clock y_offset=4 y_offset=0
```

## My Workspace
前面介绍得比较详尽了，实际SketchyBat的常用语法就是`-add`、`-script`之类的，语义理解起来更像是一个需要为其中元素设置属性、注册回掉的容器。SketchyBar本身的语法是简单的，难在回掉里的功能如何实现。
折腾SketchyBar的初衷是打造一套干净整洁的状态栏，用于构造自己的Workflow，保持专注、更容易保持心流的状态。在AI大人的协助下，前后折腾两天终于实现了预期的效果🥳。

个人Workflow状态栏[^3]效果如下图：

![Workflow Space Bar](/image/my_skybar.png)

左侧区域为Space，每个Space表示一个工作空间，前面的数字表示该工作空间所属的桌面编号（可以使用快捷键`ctrl+Num`直接跳转对应编号，也可以点击Space的图标进行跳转）。这是为零解决社区中常见的Space空间不含编号不能直观显示桌面所属的问题。其次就是每个Space后还会跟着一个小图标，该图标Icon直接表明了当前工作区间的职能，比如上图中有5个Space空间，分别表示终端、浏览器、Code/Read读写空间、工作间和杂物间，每个Space职能明晰、编号明确、语义直观，可以快速的跳转。且当前的Space工作空间会进行高亮显示，并列举其中正在运行的APP。
而右侧的区域仅保留4个关键的**item**，CPU占用率（这在编码时常用）、电池状态、时间，实际还有一个隐藏的📪信箱，当没有消息时自动隐藏。保持干净、直观的状态栏。


## References
参考文献：
[^1]: [SketchyBar官方文档](https://felixkratz.github.io/SketchyBar/features)
[^2]: [SketchyBar社区](https://github.com/FelixKratz/SketchyBar/discussions/47?sort=top)
[^3]: [个人工作流Bar参考](https://github.com/MrKeanu-V/dotfiles_mac/tree/main/sketchybar)
