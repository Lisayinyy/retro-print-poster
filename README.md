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

## 状态与限制

- 这是纯提示词插件，没有代码；仓库里也没有成片样例（生图按次计费，没有为了展示而生成）。
- 版式是固定的：一个英文单词、两段小诗、一张缩略图。需要写活动信息、标题或品牌文案的海报不适合用它。
- 模型会拼错单词或把首尾字母切掉，所以第 5 步要逐张核对文字；有问题先问用户再重做，重做同样计次。
- `skills/retro-print-poster/evals/evals.json` 里的 4 个场景用例和 `trigger-eval.json` 里的 16 条触发用例都还没有用模型实际跑过。
- 插件清单里的作者写的是 MiniMax；版式参考了小红书上流行的同类提示词。

## 参考的方法

- [obra/superpowers · writing-skills](https://github.com/obra/superpowers/blob/main/skills/writing-skills/SKILL.md)（"Testing All Skill Types"：应用场景、变体场景、缺失信息测试）。拿 8 个具体请求逐步对照 `SKILL.md` 和提示词模板走查（没有运行模型），发现三处缺口并补上：要中文诗句时模板正文仍写着"英文诗句、打字机字体、英文准确"，与 Skill 自己"补充要求不能和模板矛盾"的规则冲突；用户指定超过 7 个字母的单词时没有说怎么办；一次超过 10 张时没有说要分批。
- [anthropics/skills · skill-creator](https://github.com/anthropics/skills/blob/main/skills/skill-creator/SKILL.md)：`evals.json` 的场景用例格式，以及用"该触发 / 不该触发"的请求检验 `description`。逐条对照判断，原描述 14/16（带演出信息的复古宣传海报、只要网点滤镜这两条会误触发），补上适用范围后 16/16。
- [Agent Skills 规范](https://github.com/agentskills/agentskills/blob/main/docs/specification.mdx)：frontmatter 用 `skills-ref validate` 校验通过。
