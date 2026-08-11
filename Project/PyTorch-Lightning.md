# ⚡ PyTorch Lightning

> **The deep learning framework for professional AI researchers and machine learning engineers who need maximal flexibility without sacrificing performance at scale.**

PyTorch Lightning is the lightweight PyTorch wrapper for high-performance AI research. It organizes your PyTorch code to remove boilerplate and unlock scalability, allowing you to focus on the science—not the engineering. Lightning evolves with you as your projects go from idea to paper or production.

---

## 📋 Project Description

PyTorch Lightning is **just organized PyTorch**—it disentangles PyTorch code to decouple the science from the engineering. Built and maintained by a community of hundreds of AI researchers, research engineers, and PhDs from the world's top AI labs, Lightning structures your deep learning code into clear, reusable components.

Whether you're pretraining LLMs, fine-tuning vision models, or building your own architectures, Lightning handles the heavy lifting—multi-GPU training, mixed precision, checkpointing, logging, and more—without getting in your way.

---

## ✨ Features

### Core Capabilities

- **Full PyTorch Flexibility** – Use raw PyTorch without boilerplate. Lightning adds zero abstractions on top of pure PyTorch.
- **LightningModule** – Organizes your PyTorch code into 6 clear sections: initialization, training loop, validation loop, test loop, prediction loop, and optimizers.
- **Trainer** – Automates training, validation, and testing with built-in support for GPUs, TPUs, HPUs, and multi-node distributed training.
- **Zero Code Changes for Scaling** – Go from single GPU to multi-GPU, TPU, or multi-node without changing your code.
- **Built-in Best Practices** – Mixed precision, gradient accumulation, early stopping, learning rate finding, and more.
- **40+ Advanced Features** – Designed for professional AI research at scale.

### Key Components

| Component | Purpose |
|-----------|---------|
| **LightningModule** | Organizes your PyTorch `nn.Module` with training/validation/test logic |
| **Trainer** | Orchestrates training loops, hardware acceleration, and callbacks |
| **LightningDataModule** | Encapsulates all data loading and preprocessing logic |
| **Callbacks** | Extend functionality with hooks for logging, checkpointing, early stopping, and more |

### Supported Hardware

- **GPUs** – Single or multi-GPU (NVIDIA, AMD)
- **TPUs** – Google Cloud TPU support
- **HPUs** – Habana Gaudi accelerators
- **Multi-node** – Distributed training across multiple machines

---

## 🚀 Quick Start

Get started with Lightning in just a few minutes:

### 1. Install Lightning

```bash
pip install lightning
```

### 2. Define a LightningModule

```python
import lightning as L
import torch
import torch.nn as nn
import torch.nn.functional as F

class LitAutoEncoder(L.LightningModule):
    def __init__(self, encoder, decoder):
        super().__init__()
        self.encoder = encoder
        self.decoder = decoder

    def training_step(self, batch, batch_idx):
        x, _ = batch
        x = x.view(x.size(0), -1)
        z = self.encoder(x)
        x_hat = self.decoder(z)
        loss = F.mse_loss(x_hat, x)
        self.log("train_loss", loss)
        return loss

    def configure_optimizers(self):
        return torch.optim.Adam(self.parameters(), lr=1e-3)
```

### 3. Train the Model

```python
# Define model components
encoder = nn.Sequential(nn.Linear(28 * 28, 64), nn.ReLU(), nn.Linear(64, 3))
decoder = nn.Sequential(nn.Linear(3, 64), nn.ReLU(), nn.Linear(64, 28 * 28))

# Create LightningModule and DataLoader
autoencoder = LitAutoEncoder(encoder, decoder)
train_loader = torch.utils.data.DataLoader(MNIST(...))

# Train!
trainer = L.Trainer()
trainer.fit(autoencoder, train_loader)
```

### 4. Run on GPUs (Zero Code Changes)

```python
trainer = L.Trainer(accelerator="gpu", devices=4)  # 4 GPUs
trainer.fit(autoencoder, train_loader)
```

*For a complete walkthrough, see the [Lightning in 15 minutes](https://pytorch-lightning.readthedocs.io/en/stable/pytorch/starter/introduction.html) guide.*

---

## 📦 Installation

### With pip

```bash
pip install lightning
```

This installs the latest stable version along with PyTorch if not already present.

### With conda

```bash
conda install lightning -c conda-forge
```

This will also install the latest stable PyTorch version.

### Install with minimal dependencies (for deployment)

```bash
pip install 'lightning[pytorch]'
```


### Custom PyTorch Version

To use a specific PyTorch version, install PyTorch first from the [official PyTorch installation page](https://pytorch.org/get-started/locally/), then install Lightning.

### Build from Source (Nightly)

```bash
pip install https://github.com/Lightning-AI/lightning/archive/refs/heads/master.zip -U
```


---

## ⚙️ Configuration

### Trainer Flags

The `Trainer` class offers extensive configuration options:

```python
trainer = L.Trainer(
    accelerator="gpu",           # "cpu", "gpu", "tpu", "hpu"
    devices=4,                   # Number of devices
    precision="16-mixed",        # Mixed precision training
    max_epochs=100,              # Training epochs
    accumulate_grad_batches=4,   # Gradient accumulation
    gradient_clip_val=1.0,       # Gradient clipping
    log_every_n_steps=10,        # Logging frequency
    callbacks=[EarlyStopping()], # Callbacks
    strategy="ddp",              # Distributed strategy
)
```


### Environment Variables

| Variable | Purpose |
|----------|---------|
| `CUDA_VISIBLE_DEVICES` | Restrict GPU visibility |
| `PL_DEVICES` | Set devices for training |
| `PL_ACCELERATOR` | Set accelerator type |

### Configuration Files

Lightning supports YAML/JSON configuration files via the Lightning CLI:

```bash
python train.py --config config.yaml
```


---

## 💻 Usage Examples

### Example 1: MNIST Classifier

```python
import lightning as L
import torch
import torch.nn as nn
import torch.nn.functional as F
from torch.utils.data import DataLoader
from torchvision.datasets import MNIST
from torchvision.transforms import ToTensor

class LitClassifier(L.LightningModule):
    def __init__(self):
        super().__init__()
        self.layer_1 = nn.Linear(28 * 28, 128)
        self.layer_2 = nn.Linear(128, 10)

    def forward(self, x):
        x = x.view(x.size(0), -1)
        x = F.relu(self.layer_1(x))
        return self.layer_2(x)

    def training_step(self, batch, batch_idx):
        x, y = batch
        logits = self(x)
        loss = F.cross_entropy(logits, y)
        self.log("train_loss", loss)
        return loss

    def configure_optimizers(self):
        return torch.optim.Adam(self.parameters(), lr=1e-3)

# Train
model = LitClassifier()
trainer = L.Trainer(max_epochs=10)
trainer.fit(model, DataLoader(MNIST("./", train=True, transform=ToTensor()), batch_size=32))
```

### Example 2: Multi-GPU Training

```python
# Same model, just change the Trainer
trainer = L.Trainer(accelerator="gpu", devices=4, strategy="ddp")
trainer.fit(model, dataloader)
```


### Example 3: Transfer Learning

```python
import torchvision.models as models

class LitTransferLearning(L.LightningModule):
    def __init__(self):
        super().__init__()
        self.backbone = models.resnet50(pretrained=True)
        self.backbone.fc = nn.Linear(2048, 10)

    def training_step(self, batch, batch_idx):
        x, y = batch
        loss = F.cross_entropy(self.backbone(x), y)
        self.log("train_loss", loss)
        return loss

    def configure_optimizers(self):
        return torch.optim.Adam(self.parameters(), lr=1e-4)
```

### Example 4: Extract PyTorch Model from Checkpoint

```python
checkpoint = torch.load("model.ckpt")
model = LitModel.load_from_checkpoint(checkpoint_path="model.ckpt")
# Or extract just the nn.Module
pure_pytorch_model = model.model
```


---

## 🧪 Running Tests

PyTorch Lightning includes a comprehensive test suite. To run tests locally:

### Install Development Dependencies

```bash
pip install -e .[dev]
```

### Run Tests

```bash
pytest tests/
```

### Run Specific Test

```bash
pytest tests/trainer/test_trainer.py
```

### Code Quality Checks

```bash
pre-commit run --all-files
```

---

## 📝 Contributing

We welcome contributions of all kinds—bug fixes, new features, documentation improvements, and more.

### How to Contribute

1. **Start with an issue** – Open a GitHub issue to explain the feature and motivation.
2. **Fork the repository** – [github.com/Lightning-AI/lightning](https://github.com/Lightning-AI/lightning)
3. **Make your changes** – Follow the [design principles](https://pytorch-lightning.readthedocs.io/en/stable/generated/CONTRIBUTING.html)
4. **Add tests** – Ensure your changes are covered
5. **Submit a Pull Request** – Describe your changes and link the related issue

### Design Principles

- **No PyTorch Interference** – No abstractions on top of pure PyTorch
- **Simple Internal Code** – Clear, readable code over "ninja moves"
- **Force User Decisions to Best Practices** – Guide users toward the standard, optimal solution
- **Simple External API** – Validate API changes make sense for the wider community

### Becoming a Core Contributor

Core contributors have solid engineering skills, a good eye for user experience, and are power users of Lightning and PyTorch.

*New to open source? Check out the [Quick Open-Source Contribution Guide](https://medium.com/pytorch-lightning/quick-contribution-guide-86d977171b3a).*

---

## 📄 License

PyTorch Lightning is **open-source** and licensed under the **Apache License 2.0**.

- **Free to use** – For personal, academic, and commercial projects
- **Open source** – Full source code available on GitHub
- **Community-driven** – Built by and for the AI research community

---

## 🔗 Links

| Resource | Link |
|----------|------|
| **Website** | [lightning.ai](https://lightning.ai/) |
| **Documentation** | [lightning.ai/docs/pytorch/stable](https://lightning.ai/docs/pytorch/stable/) |
| **GitHub** | [github.com/Lightning-AI/lightning](https://github.com/Lightning-AI/lightning) |
| **PyPI** | [pypi.org/project/lightning](https://pypi.org/project/lightning) |
| **Conda** | [anaconda.org/conda-forge/lightning](https://anaconda.org/conda-forge/lightning) |
| **Discord** | [discord.gg/XncpTy7D](https://discord.gg/XncpTy7D) |
| **Blog** | [devblog.pytorchlightning.ai](https://devblog.pytorchlightning.ai) |
| **X (Twitter)** | [@PyTorchLightnin](https://twitter.com/PyTorchLightnin) |

---

*PyTorch Lightning – Train any AI model of any size. Focus on models, not engineering.*
