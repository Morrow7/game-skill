# game-skill 简介

这个文件夹用于存放一组 Codex 游戏开发相关 skills，覆盖游戏界面风格、玩法系统、引擎架构和战术射击/吃鸡玩法设计。

每个 skill 都是一个独立目录，通常包含：

- `SKILL.md`：核心说明文件，定义这个 skill 的适用场景、设计规范和验收标准。
- `agents/openai.yaml`：skill 的展示名称、简介和默认调用提示。

## 已包含的 Skills

| Skill | 简介 |
| --- | --- |
| `light-game-ui-style` | 浅色、治愈、轻松的游戏 UI 风格，包含空灵探索和温暖小镇生活模拟方向。 |
| `pixel-game-style` | 像素游戏风格，适合复古、像素 HUD、像素菜单和像素化交互界面。 |
| `sweet-girl-game-style` | 女孩甜美系风格，以粉色、黄色、白色和柔和可爱 UI 为主。 |
| `character-npc-game-style` | 偏角色/NPC 的游戏界面风格，适合对话、关系、任务、商店和角色档案。 |
| `game-skill-module` | 游戏技能模块设计，适合技能、冷却、目标选择、状态效果和 MOBA 英雄技能系统。 |
| `game-quest-module` | 游戏任务模块设计，适合主线、支线、每日任务、目标进度、奖励和任务链。 |
| `game-engine-architecture` | 游戏引擎架构设计，覆盖循环、场景、ECS、输入、渲染、物理、音频和存档。 |
| `br-sniper-weapon-system` | 吃鸡/战术射击中的高威力狙击枪系统，包含倍镜、弹道、护甲和配件。 |
| `tactical-shooter-gunplay` | 战术射击手感设计，覆盖后坐力、开镜、命中判定、换弹和移动精度。 |
| `battle-royale-zone-map` | 吃鸡安全区和地图系统，包含缩圈、航线、标点、转移和后期节奏。 |
| `br-loot-inventory-system` | 吃鸡物资和背包系统，包含拾取、弹药、配件、护甲、补给箱和快速拾取。 |
| `tactical-battle-ui-style` | 写实战术吃鸡 UI，适合 HUD、小地图、罗盘、弹药、血甲、击杀信息和倍镜界面。 |

## 使用步骤

1. 根据要设计或实现的内容，从上方列表中选择一个或多个匹配的 skill。
2. 在给 Codex 的需求中使用 `$skill-name` 显式调用，例如 `$game-skill-module`。
3. 说明目标平台、游戏类型、核心玩法、界面范围或系统范围，让 skill 能按具体场景输出。
4. 如果任务同时涉及风格和系统，可以组合多个 skill，例如 UI 风格 skill + 玩法模块 skill。
5. 根据 Codex 输出的设计规范、组件拆分、交互流程或实现建议，继续要求生成代码、原型、文档或验收清单。

## 使用示例

```text
Use $light-game-ui-style to design a cozy town life-sim inventory screen.
Use $game-skill-module to design a mobile MOBA hero skill system.
Use $br-sniper-weapon-system to design a rare battle royale sniper weapon.
```

## 组合建议

- 小镇生活模拟：`light-game-ui-style` + `character-npc-game-style` + `game-quest-module`
- 像素 RPG：`pixel-game-style` + `game-skill-module` + `game-quest-module`
- 甜美换装/收集游戏：`sweet-girl-game-style` + `character-npc-game-style`
- 移动端 MOBA：`game-skill-module` + `game-engine-architecture` + `tactical-battle-ui-style`
- 吃鸡战术射击：`tactical-shooter-gunplay` + `br-sniper-weapon-system` + `battle-royale-zone-map` + `br-loot-inventory-system` + `tactical-battle-ui-style`

## 说明

这些 skills 用于提炼通用设计语言和系统实现规范，不直接复制任何现有游戏的 Logo、角色、地图、图标、UI 布局、技能数值或专有资产。
