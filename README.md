# ComfyUI 0.38.0 on the official RunPod CUDA 13 image

This build derives from RunPod's published, pinned CUDA 13 image:

`runpod/comfyui:1.4.5-cuda13.0`

It preserves the RunPod image's OS, CUDA/PyTorch environment, startup services, and preinstalled custom nodes. It updates the baked ComfyUI application to the official `v0.38.0` tag and patches the existing `/start.sh` to append `--gpu-only` exactly once. The build stops with an error if the base image's launcher shape is not one of the two explicitly supported forms; it does not silently fall back to a new container setup.

## Files

- `Dockerfile.qwen21` — derived image definition.
- `.github/workflows/build-comfyui-qwen21-v2.yml` — manual GitHub Actions build-and-publish workflow.

## Expected output image

`ghcr.io/rocking18/comfyui-qwen21:0.38.0-cu130-gpu-only-v2`

The workflow uses `${{ github.repository_owner }}` for the actual publishing account, so it does not hardcode a username.

## Validation boundary

This package has been statically inspected and its YAML/patch logic checked locally. The container has not been built here. The GitHub Actions run must succeed before using the output, and one test Pod must confirm ComfyUI `v0.38.0`, PyTorch CUDA `13.0` / `cu130`, and the live process argument `--gpu-only` before model downloads.
