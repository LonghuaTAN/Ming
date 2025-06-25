# Ming-Lite-Omni

<p align="center">
    <img src="./figures/ant-bailing.png" width="100"/>
<p>

<p align="center">📑 <a href="https://github.com/inclusionAI/Ming">技术报告</a>｜📖<a href="https://lucaria-academy.github.io/Ming-Omni/">项目主页</a> ｜🤗 <a href="https://huggingface.co/inclusionAI/Ming-Lite-Omni">Hugging Face链接</a>｜ 🤖 <a href="https://www.modelscope.cn/models/inclusionAI/Ming-Lite-Omni">ModelScope链接</a>｜


## 引言

Ming-lite-omni 是 Ming-omni 的轻量级版本，源自 Ling-lite，28 亿激活参数。Ming-lite-omni 是一个统一的多模态模型，能够处理图像、文本、音频和视频输入，同时在语音和图像生成方面也表现出色。Ming-lite-omni 使用专用编码器从不同模态中提取 token，然后由 Ling（配备了新型模态专用路由的 MoE 架构）进行处理。这种设计使单个模型能够在统一的框架内高效地处理和融合多模态输入，无需单独构建模型、进行针对特定任务的微调或重新设计结构，从而简化了各种任务的执行。更重要的是，Ming-lite-omni 超越了传统的多模态模型，支持音频和图像生成。这是通过集成用于自然语音的高级音频解码器和用于高质量图像生成的 Ming-Lite-Uni 实现的，也使模型能够进行情景感知聊天、执行文本到语音到转化以及多种图像编辑。实验结果表明，Ming-lite-omni 为跨所有模态的统一感知和生成提供了强大的解决方案。
值得注意的是，Ming-lite-omni 是我们所知的第一个在模态支持方面与 GPT-4o 匹敌的开源模型，我们公开所有代码和模型权重，以鼓励社区的进一步研究和开发。

<p align="center">
    <img src="./figures/ming.png" width="800"/>
<p>

## 📌 更新

* [2025.06.12] 🔥  [技术报告](https://arxiv.org/abs/2506.09344) 在arxiv发布。
* [2025.05.28] 🔥  正式版发布，性能更佳，支持图像生成。
* [2025.05.04] 🔥 发布Ming-lite-omni测试版本[Ming-lite-omni-Preview](https://github.com/inclusionAI/Ming/tree/Ming-Lite-Omni-Preview)。


## 关键特征

- **统一全模态感知**: Ming-lite-omni 建立在 [Ling](https://github.com/inclusionAI/Ling)（MoE 架构 LLM）之上，它可以解决任务冲突并确保通过特定模态的路由器对来自不同模态的 token 进行一致集成。
- **统一感知与生成**: Ming-lite-omni 实现统一理解与生成，使模型能够在生成过程中理解多模态指令和用户意图，从而提升生成质量并提高跨多任务的可用性。
- **创新的生成能力**: 可以同时感知所有模态并生成高质量文本、实时语音和生动图像，在图像感知、视听交互和图像生成等多种任务中提供卓越的跨模态性能。

##  评测

Ming-lite-omni 在图像感知、视听交互和图像生成任务中均表现出色，展现出卓越的跨模态性能。具体而言，在图像感知任务中，Ming-lite-omni 仅激活 2.8B 个参数，便获得了与 Qwen2.5-VL-7B 相当的性能。它在端到端语音理解和指令跟随方面表现出色，超越了 Qwen2.5-Omni 和 Kimi-Audio。它还支持原生分辨率图像生成、编辑和风格迁移，GenEval 得分 0.64，超越 SDXL 等主流模型。在 FID 指标方面，Ming-lite-omni 达到 4.85，设定了现有方法的新 SOTA。


<p align="center">
    <img src="./figures/performance.png" width="800"/>
<p>


### 图像 benchmark
<div align="center">

| Benchmarks        | Ming-lite-omni |    Qwen2.5-VL-7B-Instruct    | InternVL2.5-8B-MPO |
|:------------------|:--------------:|:----------------------------:|:------------------:|
| AI2D              |      83.1      |             84.4             |    <b>84.5</b>     |
| HallusionBench    |  <b>55.0</b>   |             55.8             |        51.7        |
| MMBench_TEST_V11  |      80.8      |         <b>82.8</b>          |        82.0        |
| MMMU              |      56.3      |         <b>56.6</b>          |        54.8        |
| MMStar            |      64.7      |             65.3             |    <b>65.2</b>     |
| MMVet             |      71.3      |             71.6             |        68.1        |
| MathVista         |  <b>71.6</b>   |             68.1             |        67.9        |
| OCRBench          |  <b>88.4</b>   |             87.8             |        88.2        |
| Average           |      71.4      |         <b>71.5</b>          |        70.3        |

</div>


#### 百科知识 Benchmarks  
<div align="center">

| Object Recognition   | Ming-lite-omni |  Qwen2.5-VL-7B-Instruct  |
|:---------------------|:--------------:|:------------------------:|
| Plants               |   **54.96**    |           47.8           |
| Animals              |    **56.7**    |          50.85           |
| Vehicles             |     41.91      |        **42.29**         |
| Food & Ingredients   |   **62.28**    |          54.09           |
| Dishes               |    **44.3**    |          39.07           |
| General              |     91.08      |        **92.42**         |
| Average              |   **58.54**    |          54.43           |

</div>

### 视频 benchmark

<div align="center">

| Benchmarks              | Ming-lite-omni | Qwen2.5VL-7B-Instruct |
|:------------------------|:--------------:|:---------------------:|
| VideoMME                |      67.0      |      <b>67.3</b>      |
| MVBench                 |      67.7      |      <b>67.4</b>      |
| Video-MMMU              |      46.3      |      <b>47.4</b>      |
| LongVideoBench          |      56.6      |         54.7          |
| Average                 |  <b>59.4</b>   |         59.2          |

</div>
注: 所有模型均基于 128 个均匀采样的帧进行评估。

### 音频 benchmark
#### SpeechQA

<div align="center">

| Model            |    Average    | AlpacaEval  | CommonEval  |    SD-QA     |     MMSU     |  OpenBookQA  |    IFEval    |   AdvBench    |
|:-----------------|:-------------:|:-----------:|:-----------:|:------------:|:------------:|:------------:|:------------:|:-------------:|
| Qwen2-Audio-chat |     3.545     |    3.69     |    3.40     |    35.35     |    35.43     |    49.01     |    22.57     |     98.85     |
| Baichuan-Audio   |     3.695     |    4.00     |    3.39     |    49.64     |    48.80     |    63.30     |    41.32     |     86.73     |
| GLM-4-Voice      |     3.77      |    4.06     |    3.48     |    43.31     |    40.11     |    52.97     |    24.91     |     88.08     |
| Kimi-Audio       |     4.215     |    4.46     |    3.97     | <b>63.12</b> | <b>62.17</b> | <b>83.52</b> | <b>61.10</b> | <b>100.00</b> |
| Qwen2.5-Omni     |     4.21      |    4.49     |    3.93     |    55.71     |    61.32     |    81.10     |    52.87     |     99.42     |
| Ming-lite-omni   |  <b>4.34</b>  | <b>4.63</b> | <b>4.06</b> |    58.84     |    47.53     |    61.98     |    58.36     |     99.04     |
</div>

#### ASR

<div align="center">

|     Model      | aishell1 | aishell2_android | aishell2_ios | cv15_zh  | fleurs_zh | wenetspeech_meeting | wenetspeech_net | librispeech_test_clean | librispeech_test_other | multilingual_librispeech | cv15_en  | fleurs_en |  voxpopuli_v1.0_en   |
|:--------------:|:--------:|:----------------:|:------------:|:--------:|:---------:|:-------------------:|:---------------:|:----------------------:|:----------------------:|:------------------------:|:--------:|:---------:|:--------------------:|
| Ming-lite-omni |   1.47   |     **2.55**     |   **2.52**   |   6.31   |   2.96    |        5.95         |      5.46       |          1.44          |          2.80          |         **4.15**         | **6.89** | **3.39**  |       **5.80**       |
|  Qwen2.-Omni   |   1.18   |       2.75       |     2.63     | **5.20** |   3.00    |      **5.90**       |      7.70       |          1.80          |          3.40          |           7.56           |   7.60   |   4.10    |       **5.80**       |
|  Qwen2-Audio   |   1.53   |       2.92       |     2.92     |   6.90   |   7.50    |        7.16         |      8.42       |          1.60          |          3.60          |           5.40           |   8.60   |   6.90    |         6.84         |
|   Kimi-Audio   | **0.60** |       2.64       |     2.56     |   7.21   | **2.69**  |        6.28         |    **5.37**     |        **1.28**        |        **2.42**        |           5.88           |  10.31   |   4.44    |         7.97         |

</div>



### 信息检索 Benchmark
<div align="center">

| Model          | InfoSeek_H-mean | InfoSeek_unseen_question | InfoSeek_unseen_entity |
|:---------------|:---------------:|:------------------------:|:----------------------:|
| GPT-4o         |  <b>36.05</b>   |            -             |           -            |
| PaLI-X         |      22.06      |           23.5           |          20.8          |
| Qwen2.5-vl-32B |      19.35      |          20.55           |         18.28          |
| Ming-lite-omni |      27.7       |         **30.4**         |        **25.4**        |
</div>



### OCR
<div align="center">

| Model              | Ming-lite-omni | Qwen2.5-VL-7B-Instruct  |
|:-------------------|:--------------:|:-----------------------:|
| ChartQA_TEST       |      85.1      |       <b>87.3</b>       |
| DocVQA_TEST        |       93       |       <b>95.7</b>       |
| OCRBenchV2_en/zh   |    53.3/52     |    <b>56.3/57.2</b>     |
| OmniDocBench↓      | 34/<b>34.4</b> |    <b>30.8</b>/39.8     |
| TextVQA_VAL        |      82.8      |       <b>84.9</b>       |
</div>

### GUI
<div align="center">

| Model                      | Ming-lite-omni | InternVL3 8B | Qwen2.5-VL-7B-Instruct | 
|:---------------------------|:--------------:|:------------:|:----------------------:|
| ScreenSpot                 |  <b>82.1</b>   |     79.5     |         78.9*          |
| ScreenSpot-V2              |  <b>84.1</b>   |     81.4     |           -            |
| AITZ(EM)                   |  <b>66.6</b>   |      -       |         57.6*          |
</div>
注: * 表示复现的结果.



### 统一生成 Benchmark

<div align="center">

| Model          | single_object | two_object |  counting  |  colors  | position | color_attr | GENEVAL  | DPGBench  |     FID↓      |
|:---------------|:-------------:|:----------:|:----------:|:--------:|:--------:|:----------:|:--------:|:---------:|:-------------:|
| Ming-lite-omni |  **0.9875**   | **0.7727** | **0.6812** |  0.7872  |   0.31   |    0.29    | **0.64** |   81.72   |   **4.85**    |
| Metaquery-XL   |       -       |     -      |     -      |    -     |    -     |     -      |   0.61   | **82.05** |     6.02      |
| SDv2.1         |     0.98      |    0.51    |    0.44    | **0.85** |   0.07   |    0.17    |   0.50   |   68.09   |     26.96     |
| Emu3-Gen       |     0.98      |    0.71    |    0.34    |   0.81   |   0.17   |    0.21    |   0.54   |   80.60   |       -       |
| SDXL           |     0.98      |    0.74    |    0.39    | **0.85** |   0.15   |    0.23    |   0.55   |   74.65   |     8.76      |
| Janus          |     0.97      |    0.68    |    0.30    |   0.84   | **0.46** |  **0.42**  |   0.61   |   79.68   |     10.10     |
| JanusFlow      |       -       |     -      |     -      |    -     |    -     |     -      |   0.63   |   80.09   |     9.51      |

</div>

请参阅我们的技术报告以获得更全面的评测结果。


## 模型下载

可以通过Huggingface和ModelScope进行下载。
<div align="center">

|     **模型**     |  **输入模态**   | **输出模态** |                                                                       **下载链接**                                                                       |
|:--------------:|:-----------:|:--------:|:----------------------------------------------------------------------------------------------------------------------------------------------------:|
| Ming-Lite-Omni | 图片,文本,视频,音频 | 图片,文本,音频 | [🤗 HuggingFace](https://huggingface.co/inclusionAI/Ming-Lite-Omni) <br>[🤖 ModelScope](https://www.modelscope.cn/models/inclusionAI/Ming-Lite-Omni) |
</div>
如果您的所在地位于中国大陆，强烈建议您从🤖 <a href="https://www.modelscope.cn/models/inclusionAI/Ming-Lite-Omni">ModelScope</a>下载。

```shell
# huggingface
cd ./path/to/local/model
git lfs install
git clone https://huggingface.co/inclusionAI/Ming-Lite-Omni

# modelscope
cd ./path/to/local/model
pip install modelscope
modelscope download --model inclusionAI/Ming-Lite-Omni --local_dir ./
```

## 案例
更多案例参考我们的项目主页 [page](https://lucaria-academy.github.io/Ming-Omni/)。

## 使用示例

请按照模型[下载页面](#model-downloads)下载我们的模型，然后您可以参考以下代码运行 Ming-lite-omni 模型。

Python 环境依赖项安装。

```shell
pip install -r requirements.txt
pip install data/matcha_tts-0.0.5.1-cp38-cp38-linux_x86_64.whl
pip install diffusers==0.33.0
pip install nvidia-cublas-cu12==12.4.5.8  # for H20
```

注：以下示例在 NVIDIA H800-80GB & CUDA 12.2版本通过运行测试。加载 bfloat16 格式的inclusionAI/Ming-Lite-Omni 大约需要 40890MB 内存。

```python
import os
import torch
from transformers import AutoProcessor, GenerationConfig
from modeling_bailingmm import BailingMMNativeForConditionalGeneration

# build model
model = BailingMMNativeForConditionalGeneration.from_pretrained(
    "inclusionAI/Ming-Lite-Omni",
    torch_dtype=torch.bfloat16,
    low_cpu_mem_usage=True
).to("cuda")

assets_path = YOUR_ASSETS_PATH

# build processor
processor = AutoProcessor.from_pretrained("inclusionAI/Ming-Lite-Omni", trust_remote_code=True)
```

```python
# qa
messages = [
    {
        "role": "HUMAN",
        "content": [
            {"type": "text", "text": "请详细介绍鹦鹉的生活习性。"}
        ],
    },
]
# Output:

# 鹦鹉是一种非常聪明和社交性强的鸟类，它们的生活习性非常丰富和有趣。以下是一些关于鹦鹉生活习性的详细介绍：
# ### 1. **栖息地**
# 鹦鹉主要分布在热带和亚热带地区，包括非洲、亚洲、澳大利亚和南美洲。它们通常生活在森林、草原、沙漠和城市环境中。不同种类的鹦鹉对栖息地的要求有所不同，但大多数鹦鹉喜欢有丰富植被和水源的地方。
# ### 2. **饮食**
# 鹦鹉是杂食性动物，它们的饮食非常多样化。它们的食物包括种子、坚果、水果、蔬菜、花蜜和昆虫。鹦鹉的喙非常强壮，能够轻松地打开坚硬的果壳和坚果。一些鹦鹉还会吃泥土或沙子，以帮助消化和补充矿物质。
# ......

```

```python
# image qa
messages = [
    {
        "role": "HUMAN",
        "content": [
            {"type": "image", "image": os.path.join(assets_path, "flowers.jpg")},
            {"type": "text", "text": "What kind of flower is this?"},
        ],
    },
]
# Output:

# The flowers in this image are forget-me-nots. These delicate blooms are known for their small, five-petaled flowers that come in various shades of blue, pink, and white. 
```

为了能够让模型在回答之前思考，请在问题前添加以下系统提示：

```python
cot_prompt = "SYSTEM: You are a helpful assistant. When the user asks a question, your response must include two parts: first, the reasoning process enclosed in <thinking>...</thinking> tags, then the final answer enclosed in <answer>...</answer> tags. The critical answer or key result should be placed within \\boxed{}.\n"
# And your input message should be like this:
messages = [
    {
        "role": "HUMAN",
        "content": [
            {"type": "image", "image": os.path.join(assets_path, "reasoning.png")},
            {"type": "text", "text": cot_prompt + "In the rectangle $A B C D$ pictured, $M_{1}$ is the midpoint of $D C, M_{2}$ the midpoint of $A M_{1}, M_{3}$ the midpoint of $B M_{2}$ and $M_{4}$ the midpoint of $C M_{3}$. Determine the ratio of the area of the quadrilateral $M_{1} M_{2} M_{3} M_{4}$ to the area of the rectangle $A B C D$.\nChoices:\n(A) $\frac{7}{16}$\n(B) $\frac{3}{16}$\n(C) $\frac{7}{32}$\n(D) $\frac{9}{32}$\n(E) $\frac{1}{5}$"},
        ],
    },
]
# Output:
# \<think\>\nOkay, so I have this problem about a rectangle ABCD ... (thinking process omitted) ... So, the correct answer is C.\n\</think\>\n\<answer\>\\boxed{C}\</answer\>\n\n
```

```python
# video qa
messages = [
    {
        "role": "HUMAN",
        "content": [
            {"type": "video", "video": os.path.join(assets_path, "yoga.mp4")},
            {"type": "text", "text": "What is the woman doing?"},
        ],
    },
]
# Output:

# The image shows a woman performing a yoga pose on a rooftop. She's in a dynamic yoga pose, with her arms and legs extended in various positions.

```

```python
# multi-turn chat
messages = [
    {
        "role": "HUMAN",
        "content": [
            {"type": "text", "text": "中国的首都是哪里？"},
        ],
    },
    {
        "role": "ASSISTANT",
        "content": [
            {"type": "text", "text": "北京"},
        ],
    },
    {
        "role": "HUMAN",
        "content": [
            {"type": "text", "text": "它的占地面积是多少？有多少常住人口？"},
        ],
    },
]
# Output:

# 北京市的总面积约为16,410.54平方公里，常住人口约为21,542,000人。
```

```python
# Preparation for inference
text = processor.apply_chat_template(messages, add_generation_prompt=True)
image_inputs, video_inputs, audio_inputs = processor.process_vision_info(messages)
inputs = processor(
    text=[text],
    images=image_inputs,
    videos=video_inputs,
    audios=audio_inputs,
    return_tensors="pt",
)
inputs = inputs.to(model.device)
for k in inputs.keys():
    if k == "pixel_values" or k == "pixel_values_videos" or k == "audio_feats":
        inputs[k] = inputs[k].to(dtype=torch.bfloat16)

# call generate
generation_config = GenerationConfig.from_dict({'no_repeat_ngram_size': 10})
generated_ids = model.generate(
    **inputs,
    max_new_tokens=512,
    use_cache=True,
    eos_token_id=processor.gen_terminator,
    generation_config=generation_config,
)
generated_ids_trimmed = [
        out_ids[len(in_ids):] for in_ids, out_ids in zip(inputs.input_ids, generated_ids)
    ]
output_text = processor.batch_decode(
    generated_ids_trimmed, skip_special_tokens=True, clean_up_tokenization_spaces=False
)[0]
print(output_text)
```

### 音频任务

```python
# ASR
messages = [
    {
        "role": "HUMAN",
        "content": [
            {"type": "text", "text": "Please recognize the language of this speech and transcribe it. Format: oral."},
            {"type": "audio", "audio": 'data/wavs/BAC009S0915W0292.wav'},
        ],
    },
]
# we use whisper encoder for ASR task, so need modify code above
inputs = processor(
    text=[text],
    images=image_inputs,
    videos=video_inputs,
    audios=audio_inputs,
    return_tensors="pt",
    audio_kwargs={'use_whisper_encoder': True}
)

outputs = model.generate(
    **inputs,
    max_new_tokens=512,
    use_cache=True,
    eos_token_id=processor.gen_terminator,
    generation_config=generation_config,
    use_whisper_encoder=True
)

```

```python
# speech2speech
messages = [
    {
        "role": "HUMAN",
        "content": [
            {"type": "audio", "audio": 'data/wavs/speechQA_sample.wav'},
        ],
    },
]
generation_config = GenerationConfig.from_dict({
    'output_hidden_states': True,
    'return_dict_in_generate': True,
    'no_repeat_ngram_size': 10}
)

outputs = model.generate(
    **inputs,
    max_new_tokens=512,
    use_cache=True,
    eos_token_id=processor.gen_terminator,
    generation_config=generation_config,
    use_whisper_encoder=False
)

generated_ids = outputs.sequences
generated_ids_trimmed = [
    out_ids[len(in_ids):] for in_ids, out_ids in zip(inputs.input_ids, generated_ids)
]

# speechQA result
output_text = processor.batch_decode(
    generated_ids_trimmed, skip_special_tokens=True, clean_up_tokenization_spaces=False
)[0]

# for TTS
from modeling_bailing_talker import AudioDetokenizer

model_name_or_path = model.config._name_or_path
audio_detokenizer = AudioDetokenizer(
    f'{model_name_or_path}/talker/audio_detokenizer.yaml',
    flow_model_path=f'{model_name_or_path}/talker/flow.pt',
    hifigan_model_path=f'{model_name_or_path}/talker/hift.pt'
)
spk_input = torch.load('data/spks/luna.pt')
thinker_reply_part = outputs.hidden_states[0][0] + outputs.hidden_states[0][-1]
# Setting thinker_reply_part to None allows the talker to operate as a standalone TTS model, independent of the language model.
audio_tokens = model.talker.omni_audio_generation(
    output_text, 
    thinker_reply_part=thinker_reply_part, **spk_input)
waveform = audio_detokenizer.token2wav(audio_tokens, save_path='out.wav', **spk_input)

```
更多关于 ASR, SpeechQA, 和 TTS 任务的细节，参考`test_audio_tasks.py`。

### 图像生成&编辑

Ming-omni 原生支持图片生成和图片编辑，只需要在generate函数中添加相应的参数即可使用该功能。


```python
# Image generation mode currently limits the range of input pixels.
gen_input_pixels = 451584
processor.max_pixels = gen_input_pixels
processor.min_pixels = gen_input_pixels

def generate(messages, processor, model, **image_gen_param):
    text = processor.apply_chat_template(messages, add_generation_prompt=True)
    image_inputs, video_inputs, audio_inputs = processor.process_vision_info(messages)

    inputs = processor(
        text=[text],
        images=image_inputs,
        videos=video_inputs,
        audios=audio_inputs,
        return_tensors="pt",
    ).to(model.device)

    for k in inputs.keys():
        if k == "pixel_values" or k == "pixel_values_videos" or k == "audio_feats":
            inputs[k] = inputs[k].to(dtype=torch.bfloat16)
    
    print(image_gen_param)
    image = model.generate(
        **inputs,
        image_gen=True,
        **image_gen_param,
    )
    return image

```

Text-to-image
```python
messages = [
    {
        "role": "HUMAN",
        "content": [
            {"type": "text", "text": "Draw a girl with short hair."},
        ],
    }
]
image = generate(
   messages=messages, processor=processor, model=model, 
   image_gen_cfg=6.0, image_gen_steps=20, image_gen_width=480, image_gen_height=544
)
image.save("./t2i.jpg")
```

Edit
```python
messages = [
    {
        "role": "HUMAN",
        "content": [
            {"type": "image", "image": "samples/cake.jpg"},
            {"type": "text", "text": "add a candle on top of the cake"},
        ],
    }
]
image = generate(
   messages=messages, processor=processor, model=model, 
   image_gen_cfg=6.0, image_gen_steps=20, image_gen_width=512, image_gen_height=512
)
image.save("./edit.jpg")
```


## 许可和法律免责声明

本代码仓库遵循 [MIT License](./LICENSE), 法律免责声明[LEGAL.md](./LEGAL.md) 位于项目根目录下。


## 引用

如果您觉得我们的工作有所帮助，欢迎引用。

```bibtex

@misc{Mingomni2025,
      title  = {Ming-Omni: A Unified Multimodal Model for Perception and Generation}, 
      author = {Inclusion AI},
      year = {2025},
      eprint = {2506.09344},
      archivePrefix = {arXiv},
      url = {https://arxiv.org/abs/2506.09344}
}
```
