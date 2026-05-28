# ComfyUI 学习笔记：从入门到构建复杂工作流

创建时间：2026-05-24 01:01

编写:DEEPSEEK_API
标签:# 1. ComfyUI 概述与核心优势

ComfyUI 是一款基于节点图的 Stable Diffusion 图形化界面，通过连接不同的节点来构建图像生成与编辑的完整工作流。与传统的 Web UI（如 AUTOMATIC1111）相比，它具有以下突出优势：

- **可视化与模块化**：将每一个处理步骤（加载模型、提示编码、采样、VAE 解码等）拆分为独立节点，清晰展示数据流转，便于调试和复用。
- **轻量与高效**：仅占用少量 VRAM，支持生成过程的中间结果缓存，可快速试验不同参数组合，无需重新运行整个流程。
- **高级功能原生支持**：内置对 ControlNet、IP-Adapter、图像放大、视频生成、区域注意力 (Regional Prompting) 等复杂特性的支持，通过连线即可实现。
- **工作流共享与自动化**：可将整个工作流导出为 JSON 文件或 PNG 嵌入，方便分享、复现，也能通过 API 批量自动化调用。
- **活跃生态**：社区持续贡献大量自定义节点，覆盖各种模型格式、LoRA、动态提示、脸部修复等几乎所有需求。

# 2. 安装与环境配置

## 2.1 基础安装（Windows 示例）
- 下载并安装 [Python 3.10+](https://www.python.org/)（注意勾选“Add Python to PATH”）。
- 安装 Git。
- 克隆 ComfyUI 主仓库：
  ```bash
  git clone https://github.com/comfyanonymous/ComfyUI.git
  cd ComfyUI
  ```
- 安装 PyTorch（根据显卡选择 CUDA 版本，或 CPU 版本）：
  ```bash
  # CUDA 11.8 版本示例（NVIDIA 显卡）
  pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
  ```
- 安装其余依赖：
  ```bash
  pip install -r requirements.txt
  ```
- 启动：
  ```bash
  python main.py
  ```
访问 http://127.0.0.1:8188 即可打开界面。

## 2.2 模型文件放置
- **Checkpoint（大模型）**：放入 `models/checkpoints`、`models/diffusion_models` 或 `models/unet`（依据模型类型）。
- **VAE**：放入 `models/vae`。
- **LoRA / LyCORIS**：放入 `models/loras` 或 `models/lycoris`。
- **ControlNet**：放入 `models/controlnet`。
- **CLIP 模型（文本编码器）**：放入 `models/clip`。
- **Upscaler （放大模型）**：放入 `models/upscale_models`。
- **IP-Adapter**：放入 `models/ipadapter`。
- **Embeddings（embedding）**：放入 `models/embeddings`。
- **自定义节点**：通常放在 `custom_nodes` 文件夹下（部分可能需手动放入 models 对应目录，具体查阅节点文档）。

## 2.3 ComfyUI Manager 安装（强烈推荐）
ComfyUI Manager 是管理自定义节点和模型的必备工具，可一键安装、更新、禁用节点。
- 进入 `custom_nodes` 目录：
  ```bash
  cd custom_nodes
  git clone https://github.com/ltdrdata/ComfyUI-Manager.git
  ```
- 重启 ComfyUI，界面右侧会出现 Manager 按钮。
- 通过 Manager 安装缺失节点，点击 “Install Missing Custom Nodes” 跟随提示操作。

# 3. 界面初识与基础操作

- **画布**：中央区域，用于放置和连接节点。右键弹出节点菜单，可搜索添加节点；按住左键拖拽框选；Ctrl+滚轮缩放；按住中键/空格+左键平移。
- **菜单栏**：左上角 “Queue Prompt” 提交当前工作流；“Extra options” 中可管理工作流队列、批处理。
- **节点基础结构**：
  - **输入端口**：左侧彩色圆点，接收上游数据。
  - **输出端口**：右侧彩色圆点，将结果传递给下游。
  - **颜色标识**：紫色 - 文本/条件；橙色 - 图像；蓝色 - 模型；绿色 - VAE；灰色 - 潜空间；红色 - 蒙版；黄色 - 控制信号等。
- **基础节点添加**：右键 → `Add Node` → 选择类别。
- **连接**：点击输出端口拖动至输入端口。删除连接可用右键点击连线或 Shift+点击端口。
- **常用快捷键**：
  - `Ctrl+Enter`：提交当前工作流。
  - `Ctrl+S`：保存工作流为 JSON。
  - `Ctrl+O`：打开工作流文件。
  - `Ctrl+Z/Y`：撤销/重做。
  - `Delete`：删除选中节点。
  - 双击空白区域：搜索节点。
  - `Q`：快速对齐选中节点。
  - `右键节点` → `Bypass`：临时禁用该节点（数据直接通过）。

# 4. 最简文生图工作流搭建

从零构建一个基础 `文字 → 图像` 流程，需要以下节点并正确连接：

1. **加载 Checkpoint（模型）**  
   `Load Checkpoint` 节点，输出 `MODEL`、`CLIP`、`VAE` 三个数据流。

2. **提示词输入**  
   - 正面提示：`CLIP Text Encode (Prompt)` 节点，输入正向描述，将 `CLIP` 连接至其 `clip` 输入。输出 `CONDITIONING` (正条件)。
   - 负面提示：同样使用 `CLIP Text Encode (Prompt)` 节点，输入负向描述（通常为低质量、模糊、畸形等），输出负 `CONDITIONING`。

3. **采样器设置**  
   `KSampler` 节点，核心参数：
   - `model`：连接 Load Checkpoint 的 `MODEL`。
   - `positive`：连接正向 Text Encode 输出的 `CONDITIONING`。
   - `negative`：连接负向 Text Encode 输出的 `CONDITIONING`。
   - `seed`：随机种子，设为随机或固定。
   - `control_after_generate`：生成后种子变化规则（随机/递增等）。
   - `steps`：采样步数，通常 20-50。
   - `cfg`：提示词引导系数，常用 7-12。
   - `sampler_name`：采样器（如 euler、dpmpp_2m 等）。
   - `scheduler`：调度器（如 normal、karras 等）。
   - `denoise`：降噪强度，文生图通常设为 1.0。

4. **设置图像尺寸（潜空间）**  
   `Empty Latent Image` 节点，设置 `width`、`height`、`batch_size`。输出 `LATENT` 连接至 `KSampler` 的 `latent_image` 输入。

5. **解码（潜空间→像素）**  
   `VAE Decode` 节点，`samples` 接 `KSampler` 的 `LATENT` 输出，`vae` 接 Load Checkpoint 的 `VAE`。输出 `IMAGE`。

6. **预览/保存图像**  
   `Preview Image` 或 `Save Image` 节点，`images` 接 `VAE Decode` 的 `IMAGE` 输出。

**连线全貌**：
```
[Load Checkpoint] → MODEL ─┐
                          ├→ [KSampler] → LATENT → [VAE Decode] → IMAGE → [Preview Image]
          CLIP ─┐         │
                ├→ [CLIP Text Encode +] → CONDITIONING (positive) ─┘
                └→ [CLIP Text Encode -] → CONDITIONING (negative) ─┘
[Empty Latent Image] → LATENT ──────────────────────────────────────┘
```

# 5. 图生图、Inpaint 与放大

## 5.1 图生图（Image-to-Image）
- 使用 `Load Image` 节点加载一张 base 图像。
- 通过 `VAE Encode` 节点将图像转为潜空间，连接至 KSampler 的 `latent_image`（同时需要在 KSampler 中降低 `denoise` 强度，如 0.5-0.8，以保留原图结构）。
- 可以配合 `Upscale Image` (by model) 先放大再编码，获得更高质量。

## 5.2 局部重绘（Inpaint）
- 添加 `Load Image` 和 `MaskEditor` 节点（或使用外部蒙版）。
- 使用 `VAE Encode (for Inpainting)` 节点，输入图像和蒙版，输出 `LATENT` 接 KSampler。
- Checkpoint 需支持 inpainting，或使用 `InpaintModelConditioning` 节点对模型进行适配。
- 同时建议使用 `ImageScale` 等确保潜空间尺寸与 Mask 对齐。

## 5.3 高清放大（Upscaling）
**方法一：潜空间放大**
- 在 `Empty Latent Image` 之后、采样前插入 `LatentUpscale` 节点（需额外安装），直接放大潜空间。
**方法二：像素域放大 + 重采样**
- 采样生成初步图像后，使用 `Upscale Image (using Model)` 节点调用 ESRGAN 等模型放大。
- 再经过 `VAE Encode` 进入第二个 KSampler（`denoise` 0.3-0.5）进行细节增强（即 SD Upscale / Ultimate Upscale 方式）。
**方法三：Tiled Upscaler（分块放大）**
- 使用 `UltimateSDUpscale` 等自定义节点，通过分块重绘避免显存溢出。

# 6. 高级控制：ControlNet 与 IP-Adapter

## 6.1 ControlNet 使用流程
- 需要 `Load ControlNet Model` 节点（加载 cnet 模型），以及对应的预处理节点（如 `OpenposePreprocessor`、`CannyEdgePreprocessor`、`DepthPreprocessor` 等，来自 `comfyui_controlnet_aux` 等自定义节点）。
- 一般流程：
  1. `Load Image` 提供参考图像。
  2. 预处理节点生成条件图（如线稿、深度图）。
  3. `Apply ControlNet` 节点，输入 `conditioning`（来自文本编码）、`control_net`（模型）、`image`（条件图），输出更强的 `CONDITIONING`，再送入 KSampler。
  4. `strength` 参数控制影响力度（0~1），`start_percent` 和 `end_percent` 控制作用步数范围。
- 多 ControlNet 叠加：将多个 `Apply ControlNet` 节点串联，正条件依次传递。

## 6.2 IP-Adapter (Image Prompt Adapter)
- 通过 `Load IPAdapter Model` 加载 ip-adapter 模型。
- 需要配套的 CLIP Vision 模型（`Load CLIP Vision` 节点）。
- 使用 `IPAdapter Apply` 节点，融合参考图像风格或内容。
  - 输入：`ipadapter`、`clip_vision`、`model`（从 Load Checkpoint 流出，通常需要经过 `IPAdapter Model Loader` 处理或直接传入）、`image`（参考图）、`weight`（权重）。
  - 节点会自动修改模型注意力，将图像特征注入文本条件，输出新的 MODEL 给 KSampler。
- 可结合文本提示实现“参考图风格 + 文字描述内容”的混合生成。

# 7. LoRA 与模型融合

## 7.1 加载单个 LoRA
- 使用 `Load LoRA` 节点，连接到 `Load Checkpoint` 的 `MODEL` 和 `CLIP` 之后，输出修正后的 MODEL 和 CLIP。
- 可调节 `strength_model` 和 `strength_clip` 权重。

## 7.2 多个 LoRA 叠加
- 将 `Load LoRA` 节点串联（前一个输出 MODEL/CLIP 作为后一个的输入）。
- 注意叠加顺序和强度可能相互影响。

## 7.3 模型合并/切换
- 使用 `CR Apply Multi-Model` 或 `Model Merge Simple` 等节点在线融合多个 Checkpoint 的 UNET。
- 可动态切换模型，适用于不同阶段用不同模型（如基础模型生成构图，再用精修模型放大）。

# 8. 提示词的高级控制

- **动态提示权重**：`(text:1.2)` 增加权重，`[text]` 减少权重（标准 ComfyUI 支持通过 `Prompt Control` 节点或直接在 `CLIP Text Encode` 中使用语法，部分扩展节点如 `ComfyUI_Comfyroll_CustomNodes` 提供更多权重控制）。
- **区域性提示（Regional Prompting）**：使用专门的 `Regional Sampler` 节点（如 `ComfyUI_RP` 或 `Forge Couple` 节点），将画面分成不同区域，分别指定提示词并控制融合过渡。
- **提示词调度**：`Prompt Scheduling` 节点可在采样过程中动态改变提示词，实现时序变化（类似 prompt travel）。
- **从文件批量加载提示词**：使用 `Text File Loader` 节点（需安装）读取文本文件，每行一个提示，可实现批量生成。

# 9. 自定义节点生态与常用推荐

- **Efficiency Nodes**：提供高效版的采样器、编码器等，简化流程。
- **WAS Node Suite**：海量通用工具：文本处理、数学计算、图像处理混合等。
- **Derfuu Modded Nodes**：精确数学控制，用于参数化调节。
- **ComfyUI-Impact-Pack**：面部修复(Face Detailer)、分割、区域控制等。
- **ComfyUI_Comfyroll**：大量流程控制节点，动画、工作流高级交互。
- **ComfyUI-Advanced-ControlNet**：更灵活的 ControlNet 加权和时间控制。
- **ControlNet Aux**：预处理器集，用于从图像提取各种 ControlNet 条件图。
- **UltimateSDUpscale**：高质量分块放大。

# 10. 实用技巧与故障排除

- **缓存加速**：使用 `pythongosssss/ComfyUI-Custom-Scripts` 中的 `Image Feed` 缓存已生成的图片，方便对比。
- **节点对齐与整理**：选中节点按 `Q` 或右键 “Align” 可快速对齐；按住 Alt 拖动节点复制。
- **从 PNG 导入工作流**：将包含工作流元数据的生成图像直接拖入界面，或使用 “Load” 按钮选择 PNG，即可恢复完整节点图。
- **降低显存占用**：
  - 在界面 “Extra Options” 中启用 “Low VRAM” 模式。
  - 使用 `--lowvram` 启动参数（可在 `main.py` 加参数）。
  - 节点处理完立即释放模型。
- **控制速度快慢**：可调整 `batch_size` 一次出多张；采样步骤在 20-30 之间通常质量合理。
- **遇到节点缺失**：界面会显示缺失节点名称，通过 ComfyUI Manager 点击 “Install Missing Custom Nodes”，搜索并安装。
- **启动错误**：多数因 PyTorch 版本与 CUDA 不匹配或自定义节点冲突。保持 Python 版本 3.10 最佳，逐一排查新增节点。

# 11. 学习路径建议

1. **理解核心概念**：潜空间、模型、VAE、条件、采样器。
2. **搭建基础工作流**：文生图、图生图、局部重绘。
3. **掌握 Lora 与控制层**：ControlNet、IP-Adapter 的引入，实现精确控制。
4. **探索高级工作流**：风格迁移、人脸修复、区域提示、视频帧生成（配合 AnimateDiff 等）。
5. **脚本与自动化**：利用 API 或队列，批量参数生成，结合其他工具链。
6. **社区资源**：在 [ComfyUI 官方示例](https://comfyanonymous.github.io/ComfyUI_examples/) 及 CivitAI、OpenArt 等平台下载和拆解已有工作流，是快速进步的最佳方式。

通过持续实践和拆解复杂工作流，ComfyUI 将成为一个强大且高度自由的生成工具，其灵活性与复用性是传统界面难以比拟的。