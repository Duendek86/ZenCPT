# ZenCPT

ZenCPT is a miniature, single-file implementation of the GPT architecture written entirely in **Zen-C**. It features a custom autograd engine, an Adam optimizer, and a text generation pipeline.

This project is a direct port and adaptation of Andrej Karpathy's excellent [microGPT](https://gist.github.com/karpathy/8627fe009c40f57531cb18360106ce95) written in Python.

## Features

- **Pure Zen-C Implementation**: No external neural network dependencies.
- **Autograd Engine**: Built-in reverse-mode automatic differentiation graph traversing.
- **Adam Optimizer**: Includes gradient clipping and momentum updates.
- **Memory Management**: Uses a custom `zalloc.h` arena allocator for O(1) computation graph cleanup after every training step.
- **Save/Load State**: Automatically saves trained weights to `model.bin` and loads them on subsequent runs to skip retraining.
- **Dataset**: Trains on a dataset of 32,000+ names (`names.txt`) to hallucinate and generate new, similar-sounding names.

## How it works

1. **First Execution**: If `model.bin` is not found, the model will initialize random weights and begin training on `names.txt` for 1000 steps. After training, it saves the parameters to `model.bin` and performs inference.
2. **Subsequent Executions**: The model detects `model.bin`, instantly loads the trained parameters, and proceeds directly to generating text (inference mode).

## Structure
- `main.zc`: The core GPT implementation, autograd engine, and training loop.
- `names.txt`: 32,000 name dataset for training.
- `zalloc.h`: Fast arena memory allocator header.

## Acknowledgements

Huge thanks to [Andrej Karpathy](https://github.com/karpathy) for the original `microGPT` implementation that makes understanding and porting Transformers extremely accessible.
