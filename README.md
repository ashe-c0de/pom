# Pomodoro Timer

基于 Zola 的单页番茄钟，部署在 <https://ashe-wiki.github.io/25>。

## 功能

- 5 / 25 / 60 分钟三种专注时长，点击切换并立即重新计时
- 圆环进度动画，基于时间戳计算剩余时间（切换标签页后仍准确）
- 开始/结束提示音（Web Audio API 生成，无音频文件）
- Skip 按钮跳过当前计时
- 左下角显示当年剩余天数，左上角显示格言

## 项目结构

```
├── zola.toml              # 站点配置（base_url 等）
├── templates/index.html   # 唯一页面：结构 + 内联 SVG 图标
├── static/
│   ├── css/style.css      # 全部样式（配色 #248067 / #edc3ae）
│   ├── js/app.js          # 计时器、进度环、提示音
│   └── favicon.svg
├── public/                # 构建产物（已忽略，勿提交）
└── .github/workflows/deploy.yml  # 推送 main 时自动构建部署
```

## 本地开发

```bash
zola serve     # http://127.0.0.1:1111，改动自动刷新
zola build     # 输出到 public/
```

需要 [Zola](https://www.getzola.org/)。

## 自定义

| 想改什么 | 位置 |
| --- | --- |
| 右下角图标 | `templates/index.html:23` 的 `<path d="...">`（24×24 viewBox） |
| 图标颜色/大小/位置 | `static/css/style.css` 的 `.github-link` |
| 页面配色 | `style.css` 中的 `#248067`（背景）、`#edc3ae`（强调色） |
| 时长选项 | `templates/index.html` 的 `data-minutes` + `app.js` |
| 格言 | `templates/index.html` 的 `.quote-top` |
| 剩余天数文案 | `app.js` 的 `updateDaysLeft()` |
| 站点地址 | `zola.toml` 的 `base_url` |

## 链接

图标与「剩余天数」分别链接到 wiki 首页与源码仓库，改 `templates/index.html` 中对应 `<a href>`。
