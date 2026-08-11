# 🎤 Qwen3-TTS

> **The open‑source TTS powerhouse from Alibaba Cloud's Qwen team – supporting voice cloning, voice design, and ultra‑low‑latency streaming speech in 10 languages.**

Qwen3‑TTS is a state‑of‑the‑art text‑to‑speech model family developed by the Qwen team at Alibaba Cloud. Built on a discrete multi‑codebook LM architecture, it delivers expressive, stable, and controllable speech generation – from 3‑second voice cloning to natural‑language voice design and 97ms end‑to‑end latency.

Try it instantly: [ModelScope Demo](https://modelscope.cn/studios/Qwen/Qwen3-TTS) | [Hugging Face Demo](https://huggingface.co/spaces/Qwen/Qwen3-TTS)

---

## 📋 Project Description

Qwen3‑TTS is a series of open‑source speech generation models that offer comprehensive support for **voice clone**, **voice design**, and **ultra‑high‑quality human‑like speech generation** – all driven by natural‑language voice control.

Powered by the self‑developed **Qwen3‑TTS‑Tokenizer‑12Hz**, the models achieve efficient acoustic compression and high‑dimensional semantic modeling of speech signals. The **universal end‑to‑end architecture** uses a discrete multi‑codebook LM, completely bypassing the information bottlenecks and cascading errors inherent in traditional LM+DiT schemes.

With a **Dual‑Track hybrid streaming generation architecture**, a single model supports both streaming and non‑streaming generation – outputting the first audio packet immediately after a single character is input, with **end‑to‑end synthesis latency as low as 97ms**.

---

## ✨ Features

### Core Capabilities

| Feature | Description |
|---------|-------------|
| **🎯 3‑Second Voice Cloning** | Clone any voice from just 3 seconds of reference audio |
| **🎨 Voice Design** | Describe any voice in natural language (e.g., *"nervous 17‑year‑old male voice with a tenor range"*) |
| **🌍 10 Languages** | Chinese, English, Japanese, Korean, German, French, Russian, Portuguese, Spanish, Italian |
| **⚡ 97ms Ultra‑Low Latency** | End‑to‑end streaming synthesis for real‑time interactive scenarios |
| **🎭 Emotional & Prosodic Control** | Adaptive control of tone, speaking rate, and emotional expression via text semantics and instructions |
| **📦 Multiple Model Sizes** | 0.6B and 1.7B parameter versions for different resource constraints |

### Model Variants

| Model | Purpose | Streaming | Instruction Control |
|-------|---------|-----------|---------------------|
| **CustomVoice** | 9 premium timbres with style control via user instructions | ✅ | ✅ |
| **VoiceDesign** | Generate voices from natural‑language descriptions | ✅ | ✅ |
| **Base** | 3‑second rapid voice cloning; can be fine‑tuned | ✅ | – |

*All models support 10 languages.*

---

## 🚀 Quick Start

### 1. Install the Python package

```bash
pip install -U qwen-tts
```

For a clean environment (recommended):

```bash
conda create -n qwen3-tts python=3.12 -y
conda activate qwen3-tts
pip install -U qwen-tts
```



### 2. Generate speech with CustomVoice

```python
import torch
import soundfile as sf
from qwen_tts import Qwen3TTSModel

model = Qwen3TTSModel.from_pretrained(
    "Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice",
    device_map="cuda:0",
    dtype=torch.bfloat16,
    attn_implementation="flash_attention_2",
)

wavs, sr = model.generate_custom_voice(
    text="其实我真的有发现，我是一个特别善于观察别人情绪的人。",
    language="Chinese",
    speaker="Vivian",
    instruct="用特别愤怒的语气说",  # optional
)

sf.write("output.wav", wavs[0], sr)
```



### 3. Launch the local web UI (no coding required)

```bash
qwen-tts-demo Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice --ip 0.0.0.0 --port 8000
```

Then open `http://localhost:8000` in your browser.

---

## 📦 Installation

### From PyPI (recommended)

```bash
pip install -U qwen-tts
```



### From source (for development)

```bash
git clone https://github.com/QwenLM/Qwen3-TTS.git
cd Qwen3-TTS
pip install -e .
```



### FlashAttention 2 (optional, reduces GPU memory)

```bash
pip install -U flash-attn --no-build-isolation
```

If your machine has less than 96GB RAM and many CPU cores:

```bash
MAX_JOBS=4 pip install -U flash-attn --no-build-isolation
```



### Download models manually

**Via ModelScope** (recommended for users in Mainland China):

```bash
pip install -U modelscope
modelscope download --model Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice --local_dir ./Qwen3-TTS-12Hz-1.7B-CustomVoice
```

**Via Hugging Face**:

```bash
huggingface-cli download Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice --local-dir ./Qwen3-TTS-12Hz-1.7B-CustomVoice
```



---

## ⚙️ Configuration

### Model Loading Options

| Parameter | Description |
|-----------|-------------|
| `device_map` | `"cuda:0"`, `"cuda:1"`, or `"cpu"` |
| `dtype` | `torch.bfloat16` (recommended) or `torch.float16` |
| `attn_implementation` | `"flash_attention_2"` (faster, lower memory) or `"eager"` |

### CustomVoice Speakers

| Speaker | Description | Native Language |
|---------|-------------|-----------------|
| Vivian | Bright, slightly edgy young female voice | Chinese |
| Serena | Warm, gentle young female voice | Chinese |
| Uncle_Fu | Seasoned male voice with a low, mellow timbre | Chinese |
| Dylan | Youthful Beijing male voice with a clear, natural timbre | Chinese (Beijing) |
| Eric | Lively Chengdu male voice with a slightly husky brightness | Chinese (Sichuan) |
| Ryan | Dynamic male voice with strong rhythmic drive | English |
| Aiden | Sunny American male voice with a clear midrange | English |
| Ono_Anna | Playful Japanese female voice with a light, nimble timbre | Japanese |
| Sohee | Warm Korean female voice with rich emotion | Korean |



---

## 💻 Usage Examples

### Example 1: Voice Design

Create a completely new voice from a natural‑language description:

```python
import torch
import soundfile as sf
from qwen_tts import Qwen3TTSModel

model = Qwen3TTSModel.from_pretrained(
    "Qwen/Qwen3-TTS-12Hz-1.7B-VoiceDesign",
    device_map="cuda:0",
    dtype=torch.bfloat16,
    attn_implementation="flash_attention_2",
)

wavs, sr = model.generate_voice_design(
    text="哥哥，你回来啦，人家等了你好久好久了，要抱抱！",
    language="Chinese",
    instruct="体现撒娇稚嫩的萝莉女声，音调偏高且起伏明显，营造出黏人、做作又刻意卖萌的听觉效果。",
)

sf.write("voice_design.wav", wavs[0], sr)
```



### Example 2: Voice Cloning

Clone a voice from a reference audio clip (just 3 seconds needed):

```python
import torch
import soundfile as sf
from qwen_tts import Qwen3TTSModel

model = Qwen3TTSModel.from_pretrained(
    "Qwen/Qwen3-TTS-12Hz-1.7B-Base",
    device_map="cuda:0",
    dtype=torch.bfloat16,
    attn_implementation="flash_attention_2",
)

ref_audio = "https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen3-TTS-Repo/clone.wav"
ref_text = "Okay. Yeah. I resent you. I love you. I respect you. But you know what? You blew it!"

wavs, sr = model.generate_voice_clone(
    text="I am solving the equation: x = [-b ± √(b²-4ac)] / 2a? Nobody can — it's a disaster!",
    language="English",
    ref_audio=ref_audio,
    ref_text=ref_text,
)

sf.write("cloned_voice.wav", wavs[0], sr)
```



### Example 3: Voice Design → Clone (Reusable Character Voice)

Design a voice once, then reuse it like a cloned speaker:

```python
# Step 1: Design the voice
design_model = Qwen3TTSModel.from_pretrained(
    "Qwen/Qwen3-TTS-12Hz-1.7B-VoiceDesign",
    device_map="cuda:0",
    dtype=torch.bfloat16,
)

ref_wavs, sr = design_model.generate_voice_design(
    text="H-hey! You dropped your... uh... calculus notebook?",
    language="English",
    instruct="Male, 17 years old, tenor range, gaining confidence",
)

# Step 2: Build a reusable clone prompt
clone_model = Qwen3TTSModel.from_pretrained(
    "Qwen/Qwen3-TTS-12Hz-1.7B-Base",
    device_map="cuda:0",
    dtype=torch.bfloat16,
)

voice_clone_prompt = clone_model.create_voice_clone_prompt(
    ref_audio=(ref_wavs[0], sr),
    ref_text="H-hey! You dropped your... uh... calculus notebook?",
)

# Step 3: Generate multiple lines with consistent voice
sentences = [
    "No problem! I actually... kinda finished those already?",
    "What? No! I mean yes but not like... I just think you're...",
]

wavs, sr = clone_model.generate_voice_clone(
    text=sentences,
    language=["English", "English"],
    voice_clone_prompt=voice_clone_prompt,
)
```



### Example 4: Tokenizer Encode/Decode

Encode and decode audio for transport or training:

```python
import soundfile as sf
from qwen_tts import Qwen3TTSTokenizer

tokenizer = Qwen3TTSTokenizer.from_pretrained(
    "Qwen/Qwen3-TTS-Tokenizer-12Hz",
    device_map="cuda:0",
)

enc = tokenizer.encode("https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen3-TTS-Repo/tokenizer_demo_1.wav")
wavs, sr = tokenizer.decode(enc)
sf.write("decode_output.wav", wavs[0], sr)
```



### Example 5: Launch with HTTPS (for Base model microphone access)

```bash
# Generate self-signed certificate
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes -subj "/CN=localhost"

# Launch with HTTPS
qwen-tts-demo Qwen/Qwen3-TTS-12Hz-1.7B-Base \
    --ip 0.0.0.0 --port 8000 \
    --ssl-certfile cert.pem \
    --ssl-keyfile key.pem \
    --no-ssl-verify
```



---

## 🧪 Running Tests & Evaluation

### Inference Benchmark Results

**Zero‑shot speech generation (Seed‑TTS test set) – Word Error Rate (↓ lower is better):**

| Model | test‑zh | test‑en |
|-------|---------|---------|
| Seed‑TTS | 1.12 | 2.25 |
| MaskGCT | 2.27 | 2.62 |
| F5‑TTS | 1.56 | 1.83 |
| CosyVoice 3 | **0.71** | 1.45 |
| **Qwen3‑TTS‑12Hz‑1.7B‑Base** | 0.77 | **1.24** |



**Controllable speech generation (InstructTTSEval – APS ↑ higher is better):**

| Model | ZH APS | EN APS |
|-------|--------|--------|
| Gemini‑flash | 88.2 | **92.3** |
| Gemini‑pro | **89.0** | 87.6 |
| **Qwen3TTS‑12Hz‑1.7B‑CustomVoice** | 83.0 | 77.3 |
| **Qwen3TTS‑12Hz‑1.7B‑VoiceDesign** | 85.2 | 82.9 |



### Run Evaluation Locally

During evaluation, all models run with `dtype=torch.bfloat16` and `max_new_tokens=2048`. For detailed benchmark instructions, refer to the [evaluation section](https://github.com/QwenLM/Qwen3-TTS#evaluation) in the GitHub repository.

---

## 📝 Contributing

We welcome contributions! Here's how to get involved:

### Bug Reports & Feature Requests

- Open an issue on [GitHub](https://github.com/QwenLM/Qwen3-TTS/issues)
- Join the [Discord community](https://discord.gg/CV4E9rpNSD)

### Development Setup

```bash
git clone https://github.com/QwenLM/Qwen3-TTS.git
cd Qwen3-TTS
pip install -e .
```

### Code Style

- Follow PEP 8 guidelines
- Add tests for new features
- Update documentation for API changes

### Fine‑Tuning

For fine‑tuning instructions, refer to the [fine‑tuning guide](https://github.com/QwenLM/Qwen3-TTS/blob/main/finetuning).

---

## 📄 License

Qwen3‑TTS is **open‑source** and available for both academic and commercial use.

| Aspect | Details |
|--------|---------|
| **License** | Open‑source (Apache 2.0 compatible) |
| **Use** | Free for personal, academic, and commercial projects |
| **Source** | Fully available on [GitHub](https://github.com/QwenLM/Qwen3-TTS) |

*Please check the official repository for the most up‑to‑date license terms.*

---

## 🔗 Links

| Resource | Link |
|----------|------|
| **GitHub** | [github.com/QwenLM/Qwen3-TTS](https://github.com/QwenLM/Qwen3-TTS) |
| **ModelScope Demo** | [modelscope.cn/studios/Qwen/Qwen3-TTS](https://modelscope.cn/studios/Qwen/Qwen3-TTS) |
| **Hugging Face Demo** | [huggingface.co/spaces/Qwen/Qwen3-TTS](https://huggingface.co/spaces/Qwen/Qwen3-TTS) |
| **ModelScope Collection** | [modelscope.cn/collections/Qwen/Qwen3-TTS](https://modelscope.cn/collections/Qwen/Qwen3-TTS) |
| **Hugging Face Collection** | [huggingface.co/collections/Qwen/qwen3-tts](https://huggingface.co/collections/Qwen/qwen3-tts) |
| **Technical Paper** | [arXiv:2601.15621](https://arxiv.org/abs/2601.15621) |
| **Blog** | [qwen.ai/blog?id=qwen3tts-0115](https://qwen.ai/blog?id=qwen3tts-0115) |
| **Discord** | [discord.gg/CV4E9rpNSD](https://discord.gg/CV4E9rpNSD) |
| **API (DashScope)** | [help.aliyun.com/zh/model-studio/qwen-tts-realtime](https://help.aliyun.com/zh/model-studio/qwen-tts-realtime) |

---

*Qwen3‑TTS – What you imagine is what you hear.*
