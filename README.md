# 逃学威龙 · 答题惩罚椅 ⚡

复刻电影《逃学威龙》中"答题惩罚椅"经典桥段的 Web 小游戏。

## 在线体验

- **GitHub Pages**: https://weijia.github.io/quiz-chair/
- **WebDAV (latest)**: https://miya.teracloud.jp/dav/online/quiz-chair/latest/

## 游戏模式

### 模式一：答题模式 📝

内置10道常识题库，限时15秒答题的经典模式。支持导入自定义题库。

- 💣 炸弹倒计时（15秒，最后5秒闪烁警告）
- ⚡ 答错全屏震动 + 闪电特效 + 电流声 + 屏幕泛红
- ✨ 答对金色粒子撒花 + 绿色光芒 + "叮"声
- 🎯 连续答对3题触发隐藏彩蛋："你系卧底？"
- 🏁 答题结束后显示成绩评级
- 📎 支持导入自定义题库（JSON / CSV / 手动添加）

### 模式二：记分模式 🎯

独立的记分奖励/惩罚工具，用户自己出题，只负责判定对错和执行特效。

- **适用场景**：老师上课投屏、聚会游戏、活动主持
- 两个大按钮：「✅ 正确」和「❌ 错误」
- 点击"正确"：叮声 + 绿色光芒 + 金色粒子 + "好犀利啊！"
- 点击"错误"：电流声 + 全屏震动 + 闪电 + 屏幕泛红 + "电佢！"
- 连续按"正确"3次触发彩蛋："你系卧底？"
- 无倒计时，由用户自己掌控节奏
- 提供重置记分牌按钮

## 自定义题库导入

### 支持的导入方式

| 方式 | 格式 | 适用人群 | 说明 |
|------|------|----------|------|
| **JSON 文件上传** | `.json` | 有一定技术基础 | 结构化、灵活 |
| **CSV 文件上传** | `.csv` | 普通用户/老师 | Excel 导出即可，门槛最低 |
| **手动添加** | UI 表单 | 快速加几道题 | 逐题输入，适合少量补充 |

### JSON 格式

```json
{
  "title": "我的自定义题库",
  "questions": [
    {
      "q": "问题内容？",
      "options": ["选项A", "选项B", "选项C"],
      "answer": 0
    }
  ]
}
```

`answer` 为正确选项索引（0=A, 1=B, 2=C），每题固定3个选项。

### CSV 格式

用 Excel 或 WPS 编辑后另存为 CSV（UTF-8 编码）：

```
问题,选项A,选项B,选项C,正确答案
1+1=?,1,2,3,B
太阳从哪边升起?,西边,南边,东边,C
```

第5列填写正确答案字母（A/B/C）。

### 导入流程

```
开始画面 → 点击"导入自定义题库" → 弹出模态框
  ├─ 选择 JSON/CSV 文件 → 自动解析 → 显示预览
  ├─ 或切换到"手动添加"Tab → 逐题输入
  └─ 点击"导入并开始" → 验证 → 进入答题模式
```

## 数据持久化（PouchDB）

使用 [PouchDB](https://pouchdb.com/) 在浏览器本地存储所有数据，刷新页面后数据不丢失。

### 存储内容

| 数据类型 | 说明 |
|----------|------|
| **自定义题库** | 用户导入的 JSON/CSV 题库，按导入时间保存 |
| **配置信息** | 用户偏好设置（如默认模式、倒计时时长等） |
| **答题历史** | 每次答题/记分的结果记录（分数、正确率、时间） |
| **手动添加的题目** | 通过表单逐题添加的自定义题目集合 |

### PouchDB 设计

- 数据库名称：`quiz_chair_db`
- 无需后端服务器，纯浏览器端 IndexedDB 存储
- 数据随浏览器存在，清除浏览器数据会清除记录
- 可在设置中导出/清除所有数据

### 数据结构

```javascript
// 题库文档
{
  _id: 'quiz_自定义题库名称_时间戳',
  type: 'quiz_bank',
  title: '我的题库',
  questions: [...],
  createdAt: '2026-06-14T12:00:00Z',
  questionCount: 15
}

// 配置文档
{
  _id: 'config',
  type: 'config',
  defaultMode: 'quiz',       // 'quiz' | 'score'
  timerDuration: 15,          // 倒计时秒数
  lastQuizBankId: null        // 上次使用的题库ID
}

// 历史记录文档
{
  _id: 'history_时间戳',
  type: 'history',
  mode: 'quiz',               // 'quiz' | 'score'
  quizBankTitle: '默认题库',
  totalQuestions: 10,
  correctCount: 8,
  punishments: 2,
  maxStreak: 3,
  accuracy: 80,
  playedAt: '2026-06-14T12:00:00Z'
}
```

## 历史记录

- 在开始画面提供"历史记录"入口，查看过往答题/记分成绩
- 显示：模式、题库名称、正确率、被电次数、最高连对、时间
- 支持清除历史记录

## 游戏特色

- 🎬 90年代香港警校复古风格 + CRT 显示器效果 + 扫描线
- 📱 响应式设计，适配手机、电脑、电视
- 🔊 内置音效文件（Web Audio API 合成作为备用）
- 🎨 Canvas 绘制像素风电椅（带电流效果）
- 💫 CSS @keyframes 动画（震动、闪电、粒子、发光）
- 💾 PouchDB 本地持久化存储（题库、配置、历史）
- 📎 支持导入自定义题库（JSON / CSV / 手动添加）

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

### 方式一：修改代码中的内置题库

打开 `index.html`，找到 `QUESTIONS` 数组修改即可（仅限开发者）。

### 方式二：导入自定义题库（推荐）

通过页面上的"导入自定义题库"功能，上传 JSON/CSV 文件或手动添加题目。导入的题库会保存在 PouchDB 中，刷新页面后仍然可用。

## 版本管理

推送 `v*` 格式的 tag 即可触发自动部署：

```bash
git tag v1.2.0
git push origin v1.2.0
```

## 技术栈

- HTML5 + CSS3 + Vanilla JavaScript（单文件，无构建依赖）
- PouchDB（浏览器端本地数据库，IndexedDB 后端）
- Web Audio API（音效合成备用方案）
- Canvas 2D（电椅绘制）
- CSS @keyframes（震动、闪电、粒子动画）
- GitHub Actions（自动部署到 WebDAV + GitHub Pages）

## License

MIT
