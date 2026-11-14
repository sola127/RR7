# RR7

Apple Silicon / Metal 原生静态重编译研究源码，研究 Ridge Racer 7 的宿主移植、媒体桥接和运行时修复。

## 完整源码

[下载 RR7-source.zip](RR7-source.zip) · [SHA-256 校验值](SOURCE_SHA256.txt)

首次发布使用完整源码包保存目录结构。内含 65 个审核后的文本文件：手写宿主代码、42 个 SDK 文件的文本补丁、6 个新增 SDK 文件、测试、构建/本地打包脚本、架构文档、许可证及文件清单。GitHub 连接器本次没有写入权限，因此经已登录的网页上传。解压后从 `RR7/README.md` 开始阅读，文档链接以解压后的根目录为准。

**不包含游戏文件或可直接玩的 App。** 不发布原游戏可执行文件、素材、音乐、影片、游戏图标/截图、从游戏转译的 PPU/SPU 实现、密钥、解密工具、存档或游戏来源链接。构建所需本地输入应由使用者自行确保有权使用。

## 研究内容

- 720p 内部渲染，经 SMAA + MetalFX Spatial 输出 2560×1440。
- AppKit 生命周期、单实例、独立存档目录和性能图表。
- MPEG2 / ATRAC3plus、异步 AU 和回调、音频预缓冲及耗空恢复。
- FIFO 状态路由、alpha 树木边缘、有效纹理区域、夜景标量纹理采样。
- SPU 任务身份、事件和 Switch Pro 输入。

## 验证

公开文件扫描、固定上游快照上的补丁应用及逐文件比对、人工构造数据的 AU 环形队列测试通过。完整比赛、保存/载入、日文字形及所有场景未全面验收。

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
