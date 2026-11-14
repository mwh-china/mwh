# 2048 小游戏

一个纯前端单文件实现的 2048，无需构建、无需依赖、无需联网。

## 玩法

- 电脑：方向键 或 WASD
- 手机：在棋盘上滑动
- 相同数字相撞合并，合出 2048 即获胜，可继续挑战
- 最高分保存在浏览器 localStorage

## 本地运行

直接双击 `index.html` 用浏览器打开即可。

也可以起个本地服务：

```bash
cd 2048
python3 -m http.server 8000
# 浏览器打开 http://localhost:8000
```

## 推送到 GitHub

在 GitHub 网页右上角 `+` → `New repository`，仓库名填 `2048`，选 Public，**不要**勾选 "Add a README file"（本地已经有了，勾了会冲突）。

然后在项目目录执行（把 `YOUR_NAME` 换成你的 GitHub 用户名）：

```bash
cd 2048
git init
git add .
git commit -m "feat: 2048 game"
git branch -M main
git remote add origin https://github.com/YOUR_NAME/2048.git
git push -u origin main
```

若用 SSH：`git remote add origin git@github.com:YOUR_NAME/2048.git`

## 开启在线访问（GitHub Pages）

仓库 → `Settings` → 左侧 `Pages` → `Build and deployment`：
- Source: `Deploy from a branch`
- Branch: `main` / `root` → Save

等 1～2 分钟，访问：

```
https://YOUR_NAME.github.io/2048/
```

这个链接就是可以直接发给别人玩的在线地址。

## 文件说明

| 文件 | 作用 |
| --- | --- |
| `index.html` | 游戏本体（HTML + CSS + JS 全在里面） |
| `README.md` | 本说明 |
| `.gitignore` | 忽略系统垃圾文件 |

## 实现要点

- 4×4 二维数组存棋盘，按方向抽成 4 条线做「压缩 → 合并 → 补零」
- 每次有效移动后随机空格生成 2（90%）或 4（10%）
- 合并得分累加，最高分持久化
- **胜利判定**：累计得分 ≥ 2048 **或** 棋盘出现 2048 方块，任一达成即弹胜利，整局只弹一次，可选「继续挑战」或「再来一局」
- 无空格且无相邻相同数字时判定结束
