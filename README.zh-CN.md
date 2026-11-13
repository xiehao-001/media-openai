# 图像与语音生成（@eduwork/dsh-media-openai）

> 把任意 OpenAI 兼容的图像与 TTS 服务注册进成果服务，供 Studio 与聊天调用。
>
> Registers OpenAI-compatible image and TTS providers into artifact services for Studio and chat.

## 功能

不新增工具或技能，只扩展媒体 Provider：模型、音色、尺寸与服务地址来自用户或发行配置，不含任何学校默认值。依赖 @eduwork/dsh-artifact-services。

## 安装

```bash
# 在 DSH 中把本目录作为本地 bundle 安装（绝对路径）
```

安装后由 DSH 插件系统加载，条目 id 为 `media-openai`。

## 依赖

- `@eduwork/dsh-artifact-services`
- `@deepseek-ai/cordis`

## 兼容性

- `engines.dsh`: `>=0.2.1 <0.3.0`
- 与 EduWork 发行版同源，来源于 ECNU/EduWork 仓库。

## 许可

MulanPSL-2.0 AND MIT（与上游 EduWork 一致）。
