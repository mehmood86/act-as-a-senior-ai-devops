# Colab ComfyUI 3D-Print Timelapse Pipeline

This repository contains a reproducible Google Colab (free NVIDIA T4) bootstrap for ComfyUI-based AI video workflows.  It is designed to keep large model files and rendered videos on Google Drive so that they persist when Colab resets.

## Repository layout

- `notebooks/comfyui_colab_runner.ipynb` — the annotated Colab bootstrap notebook.
- `workflows/` — export ComfyUI workflow JSON files here; the included guide covers low-VRAM video options.
- `scripts/` — small local utilities for workflow and media maintenance.

## Run it in Google Colab

1. Upload this repository to GitHub or Google Drive, then open `notebooks/comfyui_colab_runner.ipynb` in [Google Colab](https://colab.research.google.com/).
2. In **Runtime → Change runtime type**, choose **T4 GPU** when it is available. Free-tier availability and session duration are not guaranteed.
3. Run the cells in order. The first cell asks for authorization to mount Drive and creates:
   - `MyDrive/ComfyUI_Storage/models/checkpoints`
   - `MyDrive/ComfyUI_Storage/models/loras`
   - `MyDrive/ComfyUI_Storage/output`
4. The next cells clone ComfyUI, point its model/output folders at Drive, install the base dependencies plus ComfyUI-Manager, and start ComfyUI with a Cloudflare public tunnel.
5. Open the printed `https://…trycloudflare.com` address. In ComfyUI, use **Manager** to install only the custom nodes required by your chosen workflow.
6. Put compatible checkpoint files in the Drive folders above, or download them through a trusted workflow/model source. Import a workflow JSON through **Workflow → Open** and queue it.

Generated files appear in `MyDrive/ComfyUI_Storage/output`, not in the temporary Colab filesystem.

## T4 / free-tier operating guidance

A T4 provides roughly 15 GB of VRAM. Start with FP8 or quantized Wan2.1/LTX-Video workflows, short clips (for example 49–81 frames), modest resolution (480p or lower), batch size 1, and sequential/offload nodes where a workflow supports them. Render small test jobs before increasing length or resolution. If CUDA out-of-memory occurs, lower frames/resolution, use a smaller model variant, and restart the runtime to clear VRAM.

Avoid committing models or output videos: those extensions are excluded in `.gitignore`. Download models only from sources you trust and review their licenses before publishing generated video.

## Tunnel note

The notebook uses Cloudflare Quick Tunnels for convenience. The URL is public to anyone who obtains it; stop the cell/runtime when finished and do not expose sensitive files or credentials through the ComfyUI instance.
