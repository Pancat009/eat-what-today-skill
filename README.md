# Eat What Today Skill

一个专门给 Agent 用的“今天吃什么”技能。完美解决你的“今天吃什么”的世界级难题！

一句话就能让 AI 给出 3 个推荐，还会附有对应图片，适合接到 OpenClaw 或任何其他 agent 工作流里。

你可以输入你城市的信息，天气，预算，辣度，甚至是心情！AI可以帮你推荐对应的菜品！


## 快速用法

```bash
python scripts/skill_cli.py 我在上海 今天午饭想点外卖 想吃粤菜 清淡一点
```

带参数覆盖自动识别：

```bash
python scripts/skill_cli.py 今天吃什么 --weather rainy --mood tired --mode takeaway --budget low --city_tag south
```

## 参数

- `--weather`：天气（下雨、炎热、寒冷等）
- `--mood`：状态/心情（累了、想清淡、想治愈）
- `--mode`：怎么吃（`takeaway` 外卖 / `dine_in` 堂食 / `cook` 自己做）
- `--budget`：预算档（`low` / `mid` / `high`）
- `--spicy`：辣度（`low` / `mid` / `high`）
- `--time_slot`：时段（早餐/午餐/晚餐/夜宵）
- `--city_tag`：口味城市标签（如 `south`、`guangdong`、`hunan`）
- `--location`：地点文本（如“上海浦东”）

## 补图（可选）

```bash
python scripts/hydrate_food_images.py --dry-run --limit 20
python scripts/hydrate_food_images.py --limit 100
python scripts/hydrate_food_images.py --limit 100 --external-ai-cmd "your_ai_command --prompt {name} --out {out_path}"
```

补图兜底顺序：
1. 先搜图 
2. 没有的话用Pollinations生图 
3. 还没有就接上你自己的的 AI 命令。

## 飞书发图片（重要！）

当在 OpenClaw 飞书环境发送本地图片时，需要遵循以下规则：

### ✅ 稳定方案（direct runtime 兼容）

1. **复制图片到 workspace**：将菜品图片复制到 `/home/azureuser/.openclaw/workspace/`
2. **使用 media 字段发送**：调用 message 工具时使用 `media` 字段传递 workspace 路径
3. **发送顺序规则**：
   - 一段文字 → 一张图 → 一段文字 → 一张图（顺序发送）
   - 禁止 Markdown 本地路径图片
   - 禁止只发文字不发图

### ⚠️ 禁止事项

- ❌ 禁止 Markdown 本地图片路径
- ❌ 禁止只发文字不发送实际图片
- ❌ 禁止一次性发送多张图片（必须逐张发送）

## 目录

- `SKILL.md`：skill 元信息和使用说明
- `scripts/skill_cli.py`：推荐入口
- `scripts/eat_what_today.py`：推荐核心逻辑
- `assets/menu_db.json`：菜品数据
- `assets/foods_image/`：本地图片

## 致谢

参考项目，感谢原作者的分享！

- https://github.com/A-kirami/whattoeat

