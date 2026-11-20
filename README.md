# 诗意复古海报（retro-print-poster）

MiniMax Code 插件：上传一张照片，用 MiniMax H3 Image（内置工具 `image_synthesize`）做成 3:4 竖版诗意复古印刷海报。

## 成片版式

| 区域 | 内容 |
|---|---|
| 上方约 1/3 | 暖白纸色留白，左右错落两段英文小诗；右上角原图缩略图，下方标注 `ORIGINAL` |
| 中部 | 横跨画面的巨大高对比衬线大写英文单词，颜色取自照片 |
| 下方 | 风格化的原照片场景，主体向上穿过大字、越过字顶进入留白 |
| 全画面 | 青 / 洋红 / 黄圆形彩色半调网点，暗密亮疏 |

单词（4–6 个字母）、两段小诗、大字颜色和光色情绪由 Agent 看图拟定，也可以自己指定；一次给多张照片时每张各出一张海报。成片为 2K、3:4，每张生成后逐项质检（拼写、主体穿字、画面衔接、缩略图）。

## 计费

活动期内（至 2026 年 11 月 20 日）MiniMax Code 每个账号共 10 次免费图片生成，每张图计 1 次；之后按 H3 Image 正常计费，Skill 会按当天日期决定是否提示免费次数。重做同样计次，不会未经同意自动重做。

## 目录

```text
.minimax-plugin/plugin.json
icon.png
skills/retro-print-poster/SKILL.md               工作流：收照片 → 看图拟定方案 → 写提示词 → 生成 → 质检 → 交付
skills/retro-print-poster/references/prompt.md   海报提示词模板与占位符说明
```

## 本地安装

```bash
cp -R retro-print-poster ~/.minimax/plugins/retro-print-poster
mcode plugin list -m local   # 应显示 retro-print-poster@local
```

## 说明

只处理用户本人或已获本人同意的照片；不生成公众人物海报。
