---
title: Getting started with PyTorch
draft: false
tags:
  - "#pytorch"
  - "#torchvision"
aliases:
---
PyTorch. Open-source machine learning library. Makes it easy to build and train Neural Networks.
## Dataset vs DataLoader
- Dataset = A storage box that holds all your data (images + labels)
- DataLoader = A smart helper that feeds data to your model in organised batches
**Simple way to think it**
- Dataset = A library with all the books
- DataLoader = A librarian who brings you books in small, manageable stacks
## Batch Size
How many examples you show to your model at once during training.
**Small batch (like 1-32):**
- Model sees fewer examples at once
- Like taking many small steps
**Large batch (like 128-512):**
- Model sees many examples at once
- Like taking fewer but bigger steps

