# 🐍 贪吃蛇 · Snake

一个零依赖、单文件的网页版贪吃蛇游戏。没有构建步骤，没有第三方库 —— 双击 `index.html` 就能玩。

![HTML5](https://img.shields.io/badge/HTML5-Canvas-orange)
![License](https://img.shields.io/badge/dependencies-0-brightgreen)

## 玩法

| 操作 | 按键 |
| --- | --- |
| 移动 | `↑` `↓` `←` `→` 或 `W` `A` `S` `D` |
| 开始 / 暂停 / 继续 | `空格` 或 `回车` |
| 手机 | 滑动屏幕转向，轻点开始/暂停 |

- 吃到红色食物得 1 分，蛇身变长。
- 每吃一个食物速度提升一档，直到上限。
- 撞墙或咬到自己即结束。
- 最高分保存在浏览器 `localStorage` 中，关掉页面也不会丢。

## 本地运行

直接双击 `index.html` 即可。若想用本地服务器：

```bash
# Python 3
python -m http.server 8000
# 然后打开 http://localhost:8000
```

## 部署到 GitHub Pages

推送完成后，在仓库页面进入 **Settings → Pages**：

1. **Source** 选择 `Deploy from a branch`
2. **Branch** 选择 `main`，目录选 `/ (root)`
3. 保存，等待一两分钟

之后就能通过 `https://<你的用户名>.github.io/<仓库名>/` 访问了。

## 项目结构

```
.
├── index.html   # 游戏本体：结构 + 样式 + 逻辑全在这一个文件里
└── README.md
```

## 实现要点

- 渲染用 Canvas 2D，按 `devicePixelRatio` 缩放，高分屏下不糊。
- 蛇身用 HSL 从头部到尾部渐变着色，头部单独画了朝向的眼睛。
- 移动采用固定步长累加器（accumulator）驱动，因此速度变化与显示器刷新率无关。
- 转向输入进队列（最多缓存 2 个），避免快速连按导致 180° 掉头自杀。
- 判定自撞时排除即将移开的蛇尾格，这是经典贪吃蛇的手感细节。

## License

MIT
