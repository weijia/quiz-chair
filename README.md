# 逃学威龙 · 答题惩罚椅 ⚡

复刻电影《逃学威龙》中"答题惩罚椅"经典桥段的 Web 小游戏。

## 在线体验

- **GitHub Pages**: https://weijia.github.io/quiz-chair/
- **WebDAV (latest)**: https://miya.teracloud.jp/dav/online/quiz-chair/latest/

## 游戏特色

- 🎬 90年代香港警校复古风格 + CRT 显示器效果
- 💣 炸弹倒计时（15秒限时答题）
- ⚡ 答错全屏震动 + 闪电特效 + 电流声
- ✨ 答对金色粒子撒花 + 绿色光芒
- 🎯 连续答对3题触发隐藏彩蛋："你系卧底？"
- 📱 响应式设计，适配手机、电脑、电视

## 如何运行

直接打开 `index.html` 即可在浏览器中运行，无需任何构建工具。

## 替换音效文件

将以下音频文件放在与 `index.html` 同一目录下：

| 文件名 | 用途 | 建议格式 |
|--------|------|----------|
| `correct.mp3` | 答对时的"叮"声 | MP3 |
| `wrong.mp3` | 答错时的电流"滋滋"声 | MP3 |
| `timeout.mp3` | 超时时的警报声 | MP3 |

> 如果没有音频文件，游戏会自动使用 Web Audio API 合成简易音效。

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
git tag v1.0.0
git push origin v1.0.0
```

## 技术栈

- HTML5 + CSS3 + Vanilla JavaScript
- Web Audio API（音效合成）
- Canvas（电椅绘制）
- CSS @keyframes（震动、闪电、粒子动画）

## License

MIT
