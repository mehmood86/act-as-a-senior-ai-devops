# 3D-print timelapse workflow guide (T4-friendly)

Store exported ComfyUI workflow JSON files in this directory. They are portable configuration, while model files belong in Google Drive and are deliberately ignored by Git.

## Importing a video workflow

1. Start the Colab runner and open its ComfyUI tunnel URL.
2. Install the workflow's documented custom nodes through **Manager**, then restart ComfyUI if prompted.
3. Copy model weights to the Drive-backed folders indicated by the workflow. Refresh the browser after adding weights.
4. Drag the workflow JSON onto the ComfyUI canvas (or use **Workflow → Open**), resolve any red/missing nodes, select your input image or prompt, and queue a small test.

## Suggested families for less than 15 GB VRAM

- **Wan2.1 image-to-video / text-to-video FP8**: prefer FP8/quantized model builds, batch size 1, and memory/offload options supplied by the nodes. It is a good route for transforming a print-progress still into a controlled, cinematic reveal.
- **LTX-Video FP8**: use the FP8 model and short, low-resolution generations first. It can be a practical choice for fast concept passes and transition clips.

Exact filenames, node packages, and licenses change by release. Follow the workflow author's model-placement instructions rather than guessing a filename.

## Timelapse prompt pattern

For text-to-video, make the temporal behavior explicit: `locked camera, FDM 3D printer building a [object], layer by layer, smooth timelapse, workshop lighting, no camera movement`. For image-to-video, use a clean render or photo of the printer/object and ask for `continuous layer-by-layer construction` while keeping motion low.

Start at 480p or below, 49–81 frames, and batch size 1. Increase only one variable at a time after a successful run. Save the final workflow JSON beside this guide, with its model and custom-node requirements documented in a short neighboring Markdown file.
