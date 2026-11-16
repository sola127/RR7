# RR7

版本 **0.3.1** · 2026-11-17 · [变更记录](CHANGELOG.md)

Apple Silicon / Metal 原生静态重编译研究源码，研究 Ridge Racer 7 的宿主移植、媒体桥接和运行时修复。

## 完整源码

[下载 RR7-source.zip](RR7-source.zip) · [SHA-256 校验值](SOURCE_SHA256.txt)

完整源码包保存目录结构。内含 73 个审核后的文本文件：手写宿主代码、43 个 SDK 文件的文本补丁、7 个新增 SDK 文件、测试、构建/本地打包脚本、架构文档、许可证及逐文件校验清单。解压后从 `RR7/README.md` 开始阅读，源码文档链接以解压后的根目录为准。

**不包含游戏文件或可直接玩的 App。** 不发布原游戏可执行文件、素材、音乐、影片、游戏图标/截图、从游戏转译的 PPU/SPU 实现、密钥、解密工具、存档或游戏来源链接。构建所需本地输入应由使用者自行确保有权使用。

## 研究内容

- 固定 720p 内部渲染，MetalFX Spatial 输出 720p / 1080p / 1440p / 4K。
- 关闭 / FXAA / SMAA / 真正的 2×、4×、8× MSAA，含颜色、深度和模板缓冲保留与 resolve。
- AppKit 生命周期、单实例、CPU / GPU / 内存 / FPS 实时图表。
- F1、⌘, 与标题栏按钮呼出设置；画面、音量/静音、手柄选择/映射、存档目录。
- 0.3.1 白名单打包、无收益资源保留、有效资源透明无损压缩与逐文件校验；完整影片与音乐保留在私有本地 App。
- MPEG2 / ATRAC3plus、异步 AU 和回调、音频预缓冲及耗空恢复。
- FIFO 状态路由、alpha 树木边缘、有效纹理区域、夜景标量纹理采样。
- SPU 任务身份、事件和 Switch Pro 输入。

## 验证

公开文件扫描、固定上游快照上的补丁应用及 50 个 SDK 文件逐一比对、人工构造数据的 AU 环形队列、设置参数与存档迁移边界测试通过。真正的 MSAA 此前已通过独立 Metal 测试。源码包中的 CI 配置是供解压后使用的模板，不代表仓库 Actions 已执行游戏验收。完整比赛、保存/载入、日文字形及所有场景未全面验收。

解压后可运行不依赖游戏的测试：

```sh
cd RR7
python3 tools/audit_public.py
c++ -std=c++17 -O1 -pthread rr7/test_au_ring.cpp -o /tmp/rr7-au-ring
/tmp/rr7-au-ring
```

## 上游与权利边界

基于 **Ned Heller / sp00nznet 的 [ps3recomp](https://github.com/sp00nznet/ps3recomp)**。版本见 [upstream.json](upstream.json)。保留上游 MIT 署名，ATRAC 组件桥接补丁保留 LGPL-2.1-or-later 条款；见 [LICENSE](LICENSE)、[NOTICE.md](NOTICE.md) 和源码包内的 licenses/。

清理和扫描降低误发布风险，不能保证消除全部法律风险。“仅供学习”不能替代授权。游戏名称仅用于识别研究对象；本项目不隶属于游戏发行商、开发商或平台厂商。源码许可证不授予原游戏内容、商标或其他第三方权利。

请勿在 Issue/PR 上传游戏内容、生成代码、图标、截图、密钥或游戏下载链接。
