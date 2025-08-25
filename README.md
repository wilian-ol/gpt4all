[![Releases](https://img.shields.io/badge/Releases-v1.0-blue)](https://github.com/wilian-ol/gpt4all/releases)

# gpt4all — Run Local LLMs on Any Device, Open-source

<img src="https://img.icons8.com/fluency/96/artificial-intelligence.png" alt="AI" align="right" />

Tags: ai-chat, llm-inference

gpt4all lets you run local large language models on laptops, servers, and edge devices. It ships as open-source software and supports commercial use. This README shows how to install, run, and build around gpt4all. Refer to the Releases page for binaries and installers: https://github.com/wilian-ol/gpt4all/releases

- Stable release assets available on the Releases page.
- Small runtime footprint for on-device inference.
- Support for CPU-only and GPU-accelerated execution.
- Simple CLI, Python bindings, and REST API adapter.

![LLM workflow](https://raw.githubusercontent.com/karpathy/neurips2020-talk/master/assets/llm.png)

## Badges

[![License](https://img.shields.io/badge/License-MIT-green)]()
[![Language](https://img.shields.io/badge/Language-Python%20%2F%20C++-yellow)]()
[![Topics](https://img.shields.io/badge/Topics-ai--chat%2Cllm--inference-lightgrey)]()

## Quick links

- Releases (binaries and installers): [Releases](https://github.com/wilian-ol/gpt4all/releases)
- Issues: use the GitHub Issues tab.
- Code: clone the repository to build or extend.

## Features

- Local inference with popular LLM formats (GGML, GGUF, ONNX).
- CLI for chat sessions and batch inference.
- Python bindings for integration in apps.
- Small memory footprint for notebooks and edge devices.
- Optional GPU acceleration using CUDA or Metal.
- Export and convert models to a portable format.

## Requirements

- OS: Linux, macOS, Windows.
- Python 3.8+ for bindings.
- A C++ compiler for optional native build.
- Optional: NVIDIA GPU and CUDA for faster inference.

## Releases and installers

Download the release asset from the Releases page and execute the appropriate file for your platform. Examples of release assets include gpt4all-windows-x64.exe and gpt4all-linux-x86_64.bin — download the file and execute it. Visit the Releases here: https://github.com/wilian-ol/gpt4all/releases

If the Releases link fails, check the repository "Releases" section on GitHub.

## Installation

Choose one flow: binary, pip, or build from source.

1) Binary (recommended for quick start)
- Visit the Releases page and pick your platform.
- Download the release asset and run it.
- On Linux:
  - chmod +x gpt4all-linux-x86_64.bin
  - ./gpt4all-linux-x86_64.bin
- On Windows:
  - Run gpt4all-windows-x64.exe and follow installer prompts.

2) Pip (Python bindings)
- Create a virtual environment.
- Install:
  ```bash
  python -m venv .venv
  source .venv/bin/activate
  pip install gpt4all
  ```
- Confirm install:
  ```bash
  python -c "import gpt4all; print(gpt4all.__version__)"
  ```

3) Build from source (advanced)
- Clone the repository:
  ```bash
  git clone https://github.com/wilian-ol/gpt4all.git
  cd gpt4all
  ```
- Install build tools:
  - Linux: build-essential, cmake
  - macOS: Xcode command line tools
  - Windows: Visual Studio with C++ workload
- Build:
  ```bash
  mkdir build && cd build
  cmake ..
  cmake --build . --config Release
  ```

## First run (CLI)

Start an interactive chat session:

```bash
gpt4all --model ./models/ggml-model.bin --chat
```

Sample flags
- --model PATH : path to model file (GGML/GGUF/ONNX)
- --threads N : CPU threads to use
- --gpu : enable GPU backend when available
- --chat : start interactive mode

Type a prompt and press Enter. Use Ctrl+C to stop.

## Python usage

The Python bindings expose a small API for loading models and running inference.

Example:

```python
from gpt4all import GPT4All

bot = GPT4All(model="./models/ggml-model.bin", threads=4)
resp = bot.generate("Write a short poem about code.")
print(resp.text)
```

Key classes and methods
- GPT4All(model, threads, gpu=False) — create an inference session
- generate(prompt, max_tokens=128, temperature=0.7) — synchronous generation
- stream(prompt, callback) — streaming generation via callback

## REST API adapter

Run the bundled REST adapter to serve the model on localhost:

```bash
gpt4all --model ./models/ggml-model.bin --api --port 8000
```

API endpoints
- POST /v1/generate
  - body: { "prompt": "Hello", "max_tokens": 100 }
  - returns: { "text": "..." }

Use this to integrate with web apps, bots, or local services.

## Model formats and conversion

Supported formats
- GGML / GGUF — optimized for CPU inference.
- ONNX — standard format for hardware accelerators.
- PyTorch checkpoints — convert to GGML/GGUF via provided tools.

Conversion utilities
- convert-to-ggml.py — convert PyTorch model to GGML
- gguf-pack — pack weights and metadata into GGUF

Example conversion:

```bash
python tools/convert-to-ggml.py --input model.pt --output models/ggml-model.bin
```

Tune quantization for memory vs quality trade-offs.

## Performance tips

- Use multiple threads on CPU for higher throughput.
- Use GPU backend on supported hardware for latency gains.
- Use quantized GGML/GGUF models for lower memory use.
- Batch prompts when possible to improve throughput.

## Security and privacy

Run models locally to keep data on-device. Use isolated environments for production deployments. Control access to the REST endpoint via firewall or local-only binding.

## Examples and templates

- Chatbot: minimal single-file Flask app that calls the REST adapter.
- CLI wrapper: extend the CLI for custom prompts, persona management, or logging.
- Stream processing: stream tokens to web clients via WebSockets.

Templates live in the examples/ directory in the repo.

## Testing

- Unit tests use pytest.
- Run tests:
  ```bash
  pytest tests
  ```
- CI runs on push and validates Linux/macOS builds.

## Contributing

- Fork the repository.
- Create a feature branch.
- Run tests and linters.
- Open a pull request with a clear changelog entry and tests.

Code style
- Python: follow PEP8.
- C++: follow repository style guide in docs/CODING.md.

## License

This project uses the MIT license. See LICENSE file in the repository.

## Maintainers

- Core: gpt4all maintainers
- Community: open to contributors via GitHub

## Troubleshooting

- If you cannot find a release asset, check the Releases page.
- If an installer fails to run, verify permissions and required system libraries.
- For model loading errors, confirm format compatibility and file integrity.

## Contacts

Open issues on GitHub for bugs and feature requests. Use Discussions for general questions and help.

## References and resources

- GGML: https://github.com/ggerganov/ggml
- ONNX: https://onnx.ai/
- Common model conversion tools included in tools/

<!-- Keep the link to Releases visible -->
[Download releases and installers](https://github.com/wilian-ol/gpt4all/releases)