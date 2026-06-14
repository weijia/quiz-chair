# 逃学威龙 · 答题惩罚椅 ⚡

复刻电影《逃学威龙》中"答题惩罚椅"经典桥段的 Web 小游戏。

## 在线体验

- **GitHub Pages**: https://weijia.github.io/quiz-chair/
- **WebDAV (latest)**: https://miya.teracloud.jp/dav/online/quiz-chair/latest/

## 游戏模式

### 模式一：答题模式 📝

内置10道常识题库，限时15秒答题的经典模式。

- 💣 炸弹倒计时（15秒，最后5秒闪烁警告）
- ⚡ 答错全屏震动 + 闪电特效 + 电流声 + 屏幕泛红
- ✨ 答对金色粒子撒花 + 绿色光芒 + "叮"声
- 🎯 连续答对3题触发隐藏彩蛋："你系卧底？"
- 🏁 10题结束后显示成绩评级

### 模式二：记分模式 🎯

独立的记分奖励/惩罚工具，用户自己出题，只负责判定对错和执行特效。

- **适用场景**：老师上课投屏、聚会游戏、活动主持
- 两个大按钮：「✅ 正确」和「❌ 错误」
- 点击"正确"：叮声 + 绿色光芒 + 金色粒子 + "好犀利啊！"
- 点击"错误"：电流声 + 全屏震动 + 闪电 + 屏幕泛红 + "电佢！"
- 连续按"正确"3次触发彩蛋："你系卧底？"
- 无倒计时，由用户自己掌控节奏
- 提供重置记分牌按钮

## 游戏特色

- 🎬 90年代香港警校复古风格 + CRT 显示器效果 + 扫描线
- 📱 响应式设计，适配手机、电脑、电视
- 🔊 内置音效文件（Web Audio API 合成作为备用）
- 🎨 Canvas 绘制像素风电椅（带电流效果）
- 💫 CSS @keyframes 动画（震动、闪电、粒子、发光）

## 项目结构

```
quiz-chair/
├── index.html              # 主页面（HTML + CSS + JS 全部内嵌）
├── sounds/                 # 音效文件目录
│   ├── correct.mp3         # 答对"叮"声
│   ├── wrong.mp3           # 答错电流"滋滋"声
│   └── timeout.mp3         # 超时警报声
├── .github/workflows/
│   └── deploy.yml          # 自动部署 workflow（WebDAV + GitHub Pages）
└── README.md
```

## 如何运行

直接打开 `index.html` 即可在浏览器中运行，无需任何构建工具。

## 替换音效文件

音效文件位于 `sounds/` 目录下，替换为自定义音频即可：

| 文件名 | 用途 | 建议格式 | 时长 |
|--------|------|----------|------|
| `sounds/correct.mp3` | 答对时的"叮"声 | MP3 | ~0.6秒 |
| `sounds/wrong.mp3` | 答错时的电流"滋滋"声 | MP3 | ~0.8秒 |
| `sounds/timeout.mp3` | 超时时的警报声 | MP3 | ~0.8秒 |

> 如果音频文件加载失败，游戏会自动使用 Web Audio API 合成简易音效作为备用。

## 修改题库

打开 `index.html`，找到 `QUESTIONS` 数组，修改题目内容即可：

```javascript
const QUESTIONS = [
  {
    q: '你的题目？',
    options: ['选项A', '选项B', '选项C'],
    answer: 0  // 正确答案的索引（0=A, 1=B, 2=C）
  },
  // 添加更多题目...
];
```

## 版本管理

推送 `v*` 格式的 tag 即可触发自动部署：

```bash
git tag v1.1.0
git push origin v1.1.0
```

## 技术栈

- HTML5 + CSS3 + Vanilla JavaScript（单文件，无构建依赖）
- Web Audio API（音效合成备用方案）
- Canvas 2D（电椅绘制）
- CSS @keyframes（震动、闪电、粒子动画）
- GitHub Actions（自动部署到 WebDAV + GitHub Pages）

## License

MIT
