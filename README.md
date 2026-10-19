# Blender Whitebox Previs

用于 Codex 的 Blender 白模预演技能：按镜头需要选择简模、关节人形或接触代理，控制构图、人物站位、动作时序、遮挡与摄影机运动。

## 适用范围

- 多人共享空间，且相对位置、朝向、遮挡或视线需要精确控制。
- 有明确构图目标的镜头，包括单人、空景和固定机位。
- 复杂运镜与多人调度。
- 救援、战斗、交接道具或机构操作等物理交互。

普通对话、常规正反打和没有特殊空间要求的简单行走，默认使用文字提示词。技能仅在明确调用或明确要求白模预演时启用。

## 安装

将本仓库克隆或复制到 Codex 的技能目录，确保 `SKILL.md` 位于 `blender-whitebox-previs` 文件夹内。

Windows PowerShell 示例：

```powershell
git clone https://github.com/yirenyan123457-droid/blender-whitebox-previs.git "$env:USERPROFILE\.codex\skills\blender-whitebox-previs"
```

若目标文件夹已有技能，请先保存现有版本，避免覆盖。

## 运行条件

- 支持加载 `SKILL.md` 的 Codex 环境。
- 可用的 Blender，以及允许 Codex 操作 Blender 的工具连接或脚本执行环境。

本仓库存放技能说明与参考标准，不包含 Blender 程序、工具服务器、教程视频或项目资产。安装技能本身不会自动配置 Blender 连接。

## 使用

在 Codex 中明确调用：

```text
$blender-whitebox-previs
为这个镜头制作 Blender 白模预演：……
时长：……；帧率：……；画幅与分辨率：……。
人物、环境与道具：……。
首帧状态：……；结尾状态：……。
希望观众看清的构图或动作：……。
```

技能先判断是否需要白模，再选择 staging、composition、action 或 mixed 模式。缺失资料按依赖处理；探索性布局需标明假设。

## 交付与验收

通常交付带版本的 `.blend` 源文件、可播放白模视频、关键审查帧、空间与相机说明及提示词交接说明。白模视频控制空间与运动，人物和环境参考控制外观。

状态使用 `DRAFT`、`REVIEW` 或 `READY_FOR_PROMPT`。必须检查实际渲染结果；仅运行成功或仅保存 `.blend` 文件不能代表预演通过。

## 文件

- [SKILL.md](SKILL.md)：适用边界、制作流程、输出契约与验收标准。
- [agents/openai.yaml](agents/openai.yaml)：Codex 展示名称、默认提示词与显式调用策略。
- [references/action-previs-standard.md](references/action-previs-standard.md)：涉及动作、接触与受力时的详细标准。
- [references/shot-routing.md](references/shot-routing.md)：镜头分流、代理选型与通用示例。
