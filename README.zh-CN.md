# wonderful.today

[English](README.md) | [简体中文](README.zh-CN.md)

## 项目简介

这是一个静态单页纪念网站，用于展示刘文龙与刘梦婷的爱情宣言、纪念图片，以及从 2011 年 11 月 12 日开始计算的相伴时长。项目采用原生 HTML、CSS 和 jQuery 实现，不包含构建工具、后端服务或前端框架。

网站地址：wonderful.today

## 页面内容

页面从上到下包含以下区域：

1. **首屏**：使用 `picture/17.jpg` 作为背景，展示两人的姓名和心形装饰。
2. **宣言**：展示摘自 2020 年 8 月 23 日婚礼的文字内容，以及署名时间。
3. **相伴时长**：使用 `picture/4.png` 作为背景，实时显示从 `2011-11-12` 起算的天、小时、分钟和秒数。
4. **页脚**：展示关系开始日期和页面最后修改时间。最后修改时间由浏览器的 `document.lastModified` 自动生成。

## 目录结构

```text
.
├── index.html              # 页面入口和主要文案
├── css/
│   ├── base.css            # 重置样式、基础排版和通用工具类
│   ├── bootstrap.css       # Bootstrap 栅格和基础组件样式
│   ├── fonts.css           # Lato-Medium 和 Fontello 字体定义
│   └── main.css            # 页面主题、区块样式和响应式规则
├── js/
│   ├── script.js           # 加载动画、背景图和模板交互初始化
│   ├── jquery-1.12.4.min.js
│   ├── jquery.countdown.min.js
│   ├── smooth-scroll.js
│   ├── venobox.min.js
│   └── clipboard.js        # 当前入口页未直接引用
├── fonts/                  # 页面字体和图标字体文件
└── picture/
    ├── 17.jpg              # 首屏背景图
    └── 4.png               # 相伴时长区域背景图
```

## 运行方式

项目是纯静态文件，可直接用浏览器打开 `index.html`。更推荐通过本地静态服务器访问，以获得更接近部署环境的行为：

```bash
cd wonderful.today
python3 -m http.server 8000
```

然后访问 <http://localhost:8000>。

项目没有 `package.json`、锁文件或构建脚本，因此不需要执行 `npm install` 或打包构建。

## 主要实现说明

### 背景图

`index.html` 中的 `.background-img` 元素内保留了 `<img>`，`js/script.js` 在页面初始化时读取其 `src`，将图片设置为 CSS 背景并隐藏原始 `<img>`。背景区域通过 `background-size: cover` 铺满对应区块。

### 加载动画

页面开始时显示 `.loader` 覆盖层。窗口触发 `load` 后，`script.js` 先淡出 `.loader-inner`，再淡出整个加载层。

### 相伴时长

`index.html` 底部内联脚本以 `2011-11-12` 为起点，每 500 毫秒重新计算经过的时间，并更新 `#elapseClock`。如果要修改纪念起始日期，应同时检查页脚的 `SINCE 2011.11.12` 文案。

### 样式与字体

- `base.css` 提供基础重置、排版和通用样式。
- `bootstrap.css` 提供栅格布局。
- `main.css` 控制首屏、宣言区、计时区、页脚及响应式表现。
- `fonts.css` 注册 Lato-Medium 和 Fontello 图标字体，心形图标使用 `.icon-heart`。

## 常见维护入口

| 修改内容 | 文件或位置 |
| --- | --- |
| 修改标题、姓名、宣言和页脚文字 | `index.html` |
| 修改相伴起始日期 | `index.html` 底部 `var strs` |
| 更换首屏背景 | `index.html` 首个 `.background-img` 的图片路径 |
| 更换计时区背景 | `index.html` 第二个 `.background-img` 的图片路径 |
| 调整颜色、字体、间距和移动端布局 | `css/main.css`、`css/base.css` |
| 调整加载动画和背景图初始化 | `js/script.js` |

## 当前注意事项

- `js/jquery.countdown.min.js` 已被引入，但当前计时器使用的是 `index.html` 中的自定义 `timeElapse` 实现。
- `js/venobox.min.js` 和 `js/smooth-scroll.js` 在 `script.js` 中被初始化，但当前入口页没有明显的相册弹窗或带 `.scroll` 类的导航链接。
- `js/clipboard.js` 当前未在 `index.html` 中引用，属于保留资源。
- `css/main.css` 还保留原始婚礼模板中事件、相册、礼物、宾客和登记表单等未使用区块的样式；删除这些样式前应确认没有计划恢复对应模块。
- 页面依赖本地图片、字体和脚本，部署时必须保持相对目录结构不变。

## 验证清单

修改页面后建议至少检查：

1. 首屏和计时区背景图是否正常显示。
2. 页面加载动画是否在资源加载完成后消失。
3. `#elapseClock` 是否持续更新，起始日期是否正确。
4. 桌面端和窄屏设备上的文字、姓名和计时器是否发生溢出。
5. 浏览器开发者工具中是否出现图片、字体或脚本加载错误。
