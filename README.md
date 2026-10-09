# Custom RunPod ComfyUI 0.38.0 — CUDA 13.0

A custom container image based on the official RunPod
ComfyUI infrastructure, configured for NVIDIA Blackwell GPUs.

## Configuration

- ComfyUI version: 0.38.0
- CUDA target: 13.0
- PyTorch CUDA build: cu130
- Startup argument: --gpu-only
- Intended GPU: NVIDIA RTX PRO 6000 Blackwell (96 GB VRAM)

## Container Image

ghcr.io/rockking18/comfyui-qwen21:0.38.0-cu130-gpu-only

## Pre-installed Components

The image retains the RunPod startup infrastructure and
pre-installed utility nodes from the upstream base image.

The startup configuration automatically adds --gpu-only
to the ComfyUI arguments if it is not already present.

## Qwen Image 2.1 Models

Model weights are not included in the container image.

Download the models into the following directories after
the Pod starts:

- Diffusion models:
  /workspace/runpod-slim/ComfyUI/models/diffusion_models/

- Text encoders and prompt enhancer:
  /workspace/runpod-slim/ComfyUI/models/text_encoders/

- VAE:
  /workspace/runpod-slim/ComfyUI/models/vae/

## Access Ports

- 8188/http — ComfyUI
- 8080/http — FileBrowser
- 8888/http — JupyterLab
- 22/tcp — SSH

## Storage

This image can be used without a Network Volume.

Models downloaded to the container disk are temporary. They
must be downloaded again when a new container starts unless
they are stored separately in persistent storage.

## Source

Based on the official RunPod ComfyUI repository:

https://github.com/runpod-workers/comfyui-base
