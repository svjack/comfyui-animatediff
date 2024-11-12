# AnimateDiff for ComfyUI

[AnimateDiff](https://github.com/guoyww/AnimateDiff/) integration for ComfyUI, adapts from [sd-webui-animatediff](https://github.com/continue-revolution/sd-webui-animatediff). Please read the original repo README for more information.

## How to Use

1. Clone this repo into `custom_nodes` folder.
2. Download motion modules and put them under `comfyui-animatediff/models/`.

- Original modules: [Google Drive](https://drive.google.com/drive/folders/1EqLC65eR1-W-sGD0Im7fkED6c8GkiNFI) | [HuggingFace](https://huggingface.co/guoyww/animatediff) | [CivitAI](https://civitai.com/models/108836) | [Baidu NetDisk](https://pan.baidu.com/s/18ZpcSM6poBqxWNHtnyMcxg?pwd=et8y)
- Community modules: [manshoety/AD_Stabilized_Motion](https://huggingface.co/manshoety/AD_Stabilized_Motion) | [CiaraRowles/TemporalDiff](https://huggingface.co/CiaraRowles/TemporalDiff)
- AnimateDiff v2 [mm_sd_v15_v2.ckpt](https://huggingface.co/guoyww/animatediff/blob/main/mm_sd_v15_v2.ckpt)

## Update 2023/09/25

#### **Motion LoRA** is now supported!

Download [motion LoRAs](https://huggingface.co/guoyww/animatediff/tree/main) and put them under `comfyui-animatediff/loras/` folder.

Note: LoRAs only work with **AnimateDiff v2** [mm_sd_v15_v2.ckpt](https://huggingface.co/guoyww/animatediff/blob/main/mm_sd_v15_v2.ckpt) module.

#### New node: `AnimateDiffLoraLoader`

<img width="370" alt="image" src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/7a9f62f7-702e-48a4-934c-bbfe1e23aff2">

Example workflow:
<img width="1280" alt="image" src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/93e7550f-4648-4482-9961-6cece5132dc9">

Workflow: [lora.json](https://github.com/ArtVentureX/comfyui-animatediff/blob/main/workflows/lora.json)

# README

## Overview

This README provides instructions on how to run a script that generates an animated GIF using the ComfyUI framework. The script downloads necessary model checkpoints and VAE (Variational Autoencoder) files, sets up the environment, and executes the workflow to produce the final GIF.

## Prerequisites

Ensure you have Python installed on your system. The script is designed to run in a script manner.

## Steps to Run the Script

### 1. Transpile the Lora JSON

First, transpile the Lora JSON file using the following command:

```bash
python -m comfy_script.transpile lora.json
```

### 2. Download Required Files

Next, download the necessary model checkpoints and VAE files using `wget`:

```bash
wget https://cdn-lfs.hf.co/repos/80/a9/80a9efd8e3732d097f2777edd953760ce288e2370fb8a8bb4803c0f8f29dca40/69ed0f5fef82b110aca51bcab73b21104242bc65d6ab4b8b2a2a94d31cad1bf0?response-content-disposition=attachment%3B+filename*%3DUTF-8%27%27mm_sd_v15_v2.ckpt%3B+filename%3D%22mm_sd_v15_v2.ckpt%22%3B&Expires=1731594908&Policy=eyJTdGF0ZW1lbnQiOlt7IkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTczMTU5NDkwOH19LCJSZXNvdXJjZSI6Imh0dHBzOi8vY2RuLWxmcy5oZi5jby9yZXBvcy84MC9hOS84MGE5ZWZkOGUzNzMyZDA5N2YyNzc3ZWRkOTUzNzYwY2UyODhlMjM3MGZiOGE4YmI0ODAzYzBmOGYyOWRjYTQwLzY5ZWQwZjVmZWY4MmIxMTBhY2E1MWJjYWI3M2IyMTEwNDI0MmJjNjVkNmFiNGI4YjJhMmE5NGQzMWNhZDFiZjA%7EcmVzcG9uc2UtY29udGVudC1kaXNwb3NpdGlvbj0qIn1dfQ__&Signature=utZR6oramTmejBIeaoomyLRLCyQUPqmLld6x21YBVF33688kEQaDnWmEFBv-2xV3NB7QKvSbo9Zf6l%7EBg%7EmwbdKUiVJLsKXuBRWlcCfamrs9DtxvDB5Nn7qqlTfklNf53t5AyUZ79fKICoHhdA7p8Zp%7EBxZZLQfb3SPyhAnr3lL6UvqaMTiX48dHJMSamHDKRkkuUVPlO7fCCK9Ftr8rbhG64tPIJcD9ga2HY05709dbd4oZXWy9Om9hPMYgkBUeRpbnMx8WnT2buG65b9bUF1wkwKipl%7EkJrnRiPDoSUH-K%7E8lW%7EJWWV9qpjb2riOen15LOO6Zp0oWOJx8ilrtUVg__&Key-Pair-Id=K3RPWS32NSSJCE -O mm_sd_v15_v2.ckpt

wget https://cdn-lfs.hf.co/repos/80/a9/80a9efd8e3732d097f2777edd953760ce288e2370fb8a8bb4803c0f8f29dca40/70ce8b9057b173b9249c48aca5d66c8aa1d8aaa040fda394e50e37f3e278195e?response-content-disposition=attachment%3B+filename*%3DUTF-8%27%27v2_lora_ZoomIn.ckpt%3B+filename%3D%22v2_lora_ZoomIn.ckpt%22%3B&Expires=1731594847&Policy=eyJTdGF0ZW1lbnQiOlt7IkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTczMTU5NDg0N319LCJSZXNvdXJjZSI6Imh0dHBzOi8vY2RuLWxmcy5oZi5jby9yZXBvcy84MC9hOS84MGE5ZWZkOGUzNzMyZDA5N2YyNzc3ZWRkOTUzNzYwY2UyODhlMjM3MGZiOGE4YmI0ODAzYzBmOGYyOWRjYTQwLzcwY2U4YjkwNTdiMTczYjkyNDljNDhhY2E1ZDY2YzhhYTFkOGFhYTA0MGZkYTM5NGU1MGUzN2YzZTI3ODE5NWU%7EcmVzcG9uc2UtY29udGVudC1kaXNwb3NpdGlvbj0qIn1dfQ__&Signature=tqt%7EFoj-qAgfh%7EiTWo%7EriZ5%7EsWQafaw4vBCx651ZIfhnb-fBKkBEuTCYWcK7pyhC1KPlbp2bSfrzXQ-v%7En1BxxN8NRZOKO%7EkqaB7YEWXDNwQnxa6yyym-Unap0oaMnpdc9WLlRDKLgLLzBxVdVVW9kXl2%7EgOJYhMnMtZ-8fq9AKQHkLPRAB1q-DAWIm14CAcKTroQs3h3eIDEmMeTmowMZmxuiLeJtZOyjMjevY33983A3OT87SnmdbzlI2rLrR5YswphaX5szzngvmxo9I1VTPPhv%7EX5yDk8wQC17Nt458yHqjJ6a4r0Ry0ek4meS1tEYdAobnnuo0BZ-1ofc0Euw__&Key-Pair-Id=K3RPWS32NSSJCE -O v2_lora_ZoomIn.ckpt

wget https://cdn-lfs.hf.co/repos/ec/ee/eceee26c5834d8a75cf04eeb17dfc06d1d5fe1d80c2f19520b148c11e2e98c45/735e4c3a447a3255760d7f86845f09f937809baa529c17370d83e4c3758f3c75?response-content-disposition=inline%3B+filename*%3DUTF-8%27%27vae-ft-mse-840000-ema-pruned.safetensors%3B+filename%3D%22vae-ft-mse-840000-ema-pruned.safetensors%22%3B&Expires=1731598817&Policy=eyJTdGF0ZW1lbnQiOlt7IkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTczMTU5ODgxN319LCJSZXNvdXJjZSI6Imh0dHBzOi8vY2RuLWxmcy5oZi5jby9yZXBvcy9lYy9lZS9lY2VlZTI2YzU4MzRkOGE3NWNmMDRlZWIxN2RmYzA2ZDFkNWZlMWQ4MGMyZjE5NTIwYjE0OGMxMWUyZTk4YzQ1LzczNWU0YzNhNDQ3YTMyNTU3NjBkN2Y4Njg0NWYwOWY5Mzc4MDliYWE1MjljMTczNzBkODNlNGMzNzU4ZjNjNzU%7EcmVzcG9uc2UtY29udGVudC1kaXNwb3NpdGlvbj0qIn1dfQ__&Signature=M8TehAX6q%7EM0cAM%7EzEmOZ2P2gsL%7ELTclcM1p2eNERQ9u9nwvVQRb4mAO8NUlvoEhBUejJe6WWR7KpWM%7ElKoRXil2O8X2UOKD1ZUh6jTtIZHUKEPMlVDD4gDeKKZejl4a4khPVF1m9az6g0GbQeqFqDBotyC7%7EjB0lssO7a5GyqwUYWBnjnTV1O49F20Z3o4tvNVTZciidYWBKZpdOY5tP-Xq1Xvk3W3wlVuUocHUzyT7-88qHCwgsRRn5b4FxjnzIdJTqAreaaChBQCkM-CjzAU0jWDirACno1d9fCdea5lEfYLlLYA68tR4afmVFy7wQyVOuP2inzsaTeOzQ02oGA__&Key-Pair-Id=K3RPWS32NSSJCE -O vae-ft-mse-840000-ema-pruned.safetensors
```

### 3. Copy Files to Appropriate Directories

Copy the downloaded files to their respective directories within the ComfyUI structure:

```bash
cp mm_sd_v15_v2.ckpt ComfyUI/custom_nodes/comfyui-animatediff/models
cp v2_lora_ZoomIn.ckpt ComfyUI/custom_nodes/comfyui-animatediff/loras
cp work/comfyui_models/checkpoints/majicmixRealistic_v7.safetensors ComfyUI/models/checkpoints
cp vae-ft-mse-840000-ema-pruned.safetensors ComfyUI/models/vae
```

### 4. Execute the Workflow

Run the following Python script to execute the workflow and generate the GIF:

```python
from comfy_script.runtime import *
load()
from comfy_script.runtime.nodes import *

with Workflow():
    motion_lora_stack = AnimateDiffLoraLoader('v2_lora_ZoomIn.ckpt', 1, None)
    motion_module = AnimateDiffModuleLoader('mm_sd_v15_v2.ckpt', motion_lora_stack)
    model, clip, _ = CheckpointLoaderSimple("majicmixRealistic_v7.safetensors")
    conditioning = CLIPTextEncode('photo of coastline, rocks, storm weather, wind, waves, lightning, 8k uhd, dslr, soft lighting, high quality, film grain, Fujifilm XT3', clip)
    conditioning2 = CLIPTextEncode('blur, haze, deformed iris, deformed pupils, semi-realistic, cgi, 3d, render, sketch, cartoon, drawing, anime, mutated hands and fingers, deformed, distorted, disfigured, poorly drawn, bad anatomy, wrong anatomy, extra limb, missing limb, floating limbs, disconnected limbs, mutation, mutated, ugly, disgusting, amputation', clip)
    latent = EmptyLatentImage(512, 512, 1)
    latent = AnimateDiffSampler(motion_module, 'default', 14, model, 45987230, 25, 7.5, 'ddim', 'ddim_uniform', conditioning, conditioning2, latent, 1, None)
    vae = VAELoader('vae-ft-mse-840000-ema-pruned.safetensors')
    image = VAEDecode(latent, vae)
    AnimateDiffCombine(image, 8, 0, False, 'AnimateDiff', 'image/gif', False)
```

### 5. Locate the Generated GIF

The generated GIF will be located in the `ComfyUI/temp` directory. You can list the contents of this directory to verify the presence of the GIF:

```bash
ls ComfyUI/temp
```

![AnimateDiff_00001_](https://github.com/user-attachments/assets/f855dbee-a891-4039-93c3-647ae5ff221e)

# AnimateDiff Workflow README (For simple motion tuned generation)

This README provides an overview of the AnimateDiff workflow, which is designed to generate animated images using the ComfyUI framework. The workflow includes two main scripts: one for the original workflow and another for a workflow that incorporates a LoRA (Low-Rank Adaptation) model.

## Prerequisites

Before running the workflow, ensure that you have the following files in the appropriate directories:

1. **Motion Module**: `v3_sd15_mm.ckpt` should be placed in the `ComfyUI/custom_nodes/comfyui-animatediff/models` directory.
2. **Checkpoint Model**: `majicmixRealistic_v7.safetensors` should be available in the expected location.
3. **VAE Model**: `vae-ft-mse-840000-ema-pruned.safetensors` should be available in the expected location.
4. **LoRA Model**: `500_man_running_temporal_unet.safetensors` should be available in the expected location if you plan to use the LoRA-enhanced workflow.

## Original Workflow

The original workflow generates an animated image of a man running. The steps are as follows:

1. **Load the Motion Module**: The `AnimateDiffModuleLoader` node loads the motion module from `v3_sd15_mm.ckpt`.
2. **Load the Checkpoint Model**: The `CheckpointLoaderSimple` node loads the `majicmixRealistic_v7.safetensors` model.
3. **Encode Text Prompts**: Two text prompts are encoded using the `CLIPTextEncode` node:
   - The first prompt describes a man running.
   - The second prompt includes negative conditions to avoid undesirable features.
4. **Generate Latent Image**: An empty latent image is created using the `EmptyLatentImage` node.
5. **Sample the Latent Image**: The `AnimateDiffSampler` node samples the latent image using the motion module and the encoded text prompts.
6. **Load the VAE Model**: The `VAELoader` node loads the `vae-ft-mse-840000-ema-pruned.safetensors` model.
7. **Decode the Latent Image**: The `VAEDecode` node decodes the latent image into a visual format.
8. **Combine and Export**: The `AnimateDiffCombine` node combines the frames into an animated GIF.

### Script

```python
from comfy_script.runtime import *
load()
from comfy_script.runtime.nodes import *
with Workflow():
    motion_module = AnimateDiffModuleLoader('v3_sd15_mm.ckpt')
    model, clip, _ = CheckpointLoaderSimple("majicmixRealistic_v7.safetensors")
    conditioning = CLIPTextEncode('a man is running', clip)
    conditioning2 = CLIPTextEncode('blur, haze, deformed iris, deformed pupils, semi-realistic, cgi, 3d, render, sketch, cartoon, drawing, anime, mutated hands and fingers, deformed, distorted, disfigured, poorly drawn, bad anatomy, wrong anatomy, extra limb, missing limb, floating limbs, disconnected limbs, mutation, mutated, ugly, disgusting, amputation', clip)
    latent = EmptyLatentImage(512, 512, 1)
    latent = AnimateDiffSampler(motion_module, 'default', 14, model, 45987230, 25, 7.5, 'ddim', 'ddim_uniform', conditioning, conditioning2, latent, 1, None)
    vae = VAELoader('vae-ft-mse-840000-ema-pruned.safetensors')
    image = VAEDecode(latent, vae)
    AnimateDiffCombine(image, 8, 0, False, 'AnimateDiff', 'image/gif', False)
```

![AnimateDiff_00010_](https://github.com/user-attachments/assets/87f2f60b-66fc-4930-a678-16ed2e5ba6a3)


## Workflow with LoRA (Temporal Directory)

This workflow is similar to the original but incorporates a LoRA model to enhance the temporal consistency of the animation.

1. **Load the LoRA Model**: The `AnimateDiffLoraLoader` node loads the `500_man_running_temporal_unet.safetensors` LoRA model.
2. **Load the Motion Module**: The `AnimateDiffModuleLoader` node loads the motion module from `v3_sd15_mm.ckpt`, incorporating the LoRA model.
3. **Load the Checkpoint Model**: The `CheckpointLoaderSimple` node loads the `majicmixRealistic_v7.safetensors` model.
4. **Encode Text Prompts**: A single text prompt is encoded using the `CLIPTextEncode` node, describing a man running on the road.
5. **Generate Latent Image**: An empty latent image is created using the `EmptyLatentImage` node.
6. **Sample the Latent Image**: The `AnimateDiffSampler` node samples the latent image using the motion module and the encoded text prompt.
7. **Load the VAE Model**: The `VAELoader` node loads the `vae-ft-mse-840000-ema-pruned.safetensors` model.
8. **Decode the Latent Image**: The `VAEDecode` node decodes the latent image into a visual format.
9. **Combine and Export**: The `AnimateDiffCombine` node combines the frames into an animated GIF.

### Script

```python
from comfy_script.runtime import *
load()
from comfy_script.runtime.nodes import *
with Workflow():
    motion_lora_stack = AnimateDiffLoraLoader('500_man_running_temporal_unet.safetensors', 1, None)
    motion_module = AnimateDiffModuleLoader('v3_sd15_mm.ckpt', motion_lora_stack)
    model, clip, _ = CheckpointLoaderSimple("majicmixRealistic_v7.safetensors")
    conditioning = CLIPTextEncode('a man is running on the road.', clip)
    conditioning2 = CLIPTextEncode('', clip)
    latent = EmptyLatentImage(512, 512, 1)
    latent = AnimateDiffSampler(motion_module, 'default', 14, model, 45987230, 25, 7.5, 'ddim', 'ddim_uniform', conditioning, conditioning2, latent, 1, None)
    vae = VAELoader('vae-ft-mse-840000-ema-pruned.safetensors')
    image = VAEDecode(latent, vae)
    AnimateDiffCombine(image, 8, 0, False, 'AnimateDiff', 'image/gif', False)
```

![AnimateDiff_00009_](https://github.com/user-attachments/assets/1bf45bce-b34a-4138-9573-fa0300327905)


## Running the Workflow

To run the workflow, ensure that all the required files are in the correct directories and execute the script in your ComfyUI environment. The output will be an animated GIF of a man running, with or without the LoRA enhancement depending on the script you choose to run.

## Notes

- Ensure that the paths to the models and files are correct.
- The workflow is designed to be run in a ComfyUI environment with the necessary nodes and dependencies installed.
- The LoRA-enhanced workflow is expected to produce more temporally consistent animations.

For any issues or further customization, refer to the ComfyUI documentation or community resources.

## Conclusion

This script automates the process of downloading necessary models, setting up the environment, and executing the workflow to generate an animated GIF using the ComfyUI framework. Ensure all prerequisites are met before running the script.

Samples:

<table>
<tr>
<td>
<img width="512" alt="image" src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/2c5aa25e-0682-481f-8842-066c5b988864">
</td>
</tr>
<tr>
<td>
<img width="512" alt="image" src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/adfbad45-3ba5-42e3-9bee-d2b83f43989c">
</td>
</tr>
<tr>
<td>
<img width="512" alt="image" src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/8e484c74-c691-4d1c-9514-719dbfe3a0b5">
</td>
</tr>
<tr>
<td>
<img width="512" alt="image" src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/4921a335-9207-4a7b-9d66-61a5d76e3179">
</td>
</tr>
</table>

## Update 2023/09/21

#### **Sliding Window** is now available!

The sliding window feature enables you to generate GIFs without a frame length limit. It divides frames into smaller batches with a slight overlap. This feature is activated automatically when generating more than 16 frames. To modify the trigger number and other settings, utilize the `SlidingWindowOptions` node. See the [sample workflow](#long-duration-with-sliding-window) bellow.

## Nodes

#### AnimateDiffLoader

<img width="370" alt="image" src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/9d756d01-ea45-4d1c-8e48-56f2725c7ca1">

#### AnimateDiffSampler

- Mostly the same with `KSampler`
- `motion_module`: use `AnimateDiffLoader` to load the motion module
- `inject_method`: should left default
- `frame_number`: animation length
- `latent_image`: You can pass an `EmptyLatentImage`
- `sliding_window_opts`: custom sliding window options

<img width="370" alt="image" src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/a352195d-f40c-494d-bd3d-30ee88174b88">

#### AnimateDiffCombine

- Combine GIF frames and produce the GIF image
- `frame_rate`: number of frame per second
- `loop_count`: use 0 for infinite loop
- `save_image`: should GIF be saved to disk
- `format`: supports `image/gif`, `image/webp` (better compression), `video/webm`, `video/h264-mp4`, `video/h265-mp4`. To use video formats, you'll need [ffmpeg](https://ffmpeg.org/download.html) installed and available in **`PATH`**

<img width="370" alt="image" src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/381c5acc-06ef-43da-ada0-3dc76f37a3e4">

#### SlidingWindowOptions

Custom sliding window options

- `context_length`: number of frame per _window_. Use **16** to get the best results. Reduce it if you have low VRAM.
- `context_stride`:
  - 1: sampling every frame
  - 2: sampling every frame then every second frame
  - 3: sampling every frame then every second frame then every third frames
  - ...
- `context_overlap`: overlap frames between each window slice
- `closed_loop`: make the GIF a closed loop, will add more sampling step

<img width="370" alt="image" src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/6679a8dd-bf96-419f-8934-ea2b046dd23c">

#### LoadVideo

Load GIF or video as images. Usefull to load a GIF as ControlNet input.

- `frame_start`: Skip some begining frames and start at `frame_start`
- `frame_limit`: Only take `frame_limit` frames

<img width="370" alt="image" src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/684176d5-6369-4a27-9f33-e721e0fe1876">

## Workflows

### Simple txt2gif

<img width="1280" alt="image" src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/b7164539-bc58-4ef9-b178-d914e833805e">

Workflow: [simple.json](https://github.com/ArtVentureX/comfyui-animatediff/blob/main/workflows/simple.json)

Samples:

![animate_diff_01](https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/97efb96f-3d3d-4976-8789-78b88f89b2eb)

![animate_diff_02](https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/c39b26f7-a2af-4dc4-902f-c363e2e6f39a)

### Long duration with sliding window

<img width="1280" alt="image" src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/0f8bfb87-83cb-4119-9777-e3948ec0cb5c">

Workflow: [sliding-window.json](https://github.com/ArtVentureX/comfyui-animatediff/blob/main/workflows/sliding-window.json)

Samples:

<table>
<tr>
<td>
<img width="512" alt="image" src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/e1da7a66-e615-475d-9400-41eff484ad49">
</td>
</tr>
<tr>
<td>
<img width="768" alt="image" src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/4faa7e5e-cdaa-49da-8759-46d779c0e0b6">
</td>
</tr>
</table>

### Latent upscale

Upscale latent output using `LatentUpscale` then do a 2nd pass with `AnimateDiffSampler`.

<img width="1280" alt="image" src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/987a1c5a-c1f8-4b24-8c62-f14496261d6c">

Workflow: [latent-upscale.json](https://github.com/ArtVentureX/comfyui-animatediff/blob/main/workflows/latent-upscale.json)

Samples:
![animate_diff_upscale](https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/f363f6f8-3117-4fa8-bca9-62f6a6e38ce7)

### Using with ControlNet

You will need following additional nodes:

- [Kosinkadink/ComfyUI-Advanced-ControlNet](https://github.com/Kosinkadink/ComfyUI-Advanced-ControlNet): Apply different weight for each latent in batch
- [Fannovel16/comfyui_controlnet_aux](https://github.com/Fannovel16/comfyui_controlnet_aux): ControlNet preprocessors

#### Animate with starting and ending images

- Use `LatentKeyframe` and `TimestampKeyframe` from [ComfyUI-Advanced-ControlNet](https://github.com/Kosinkadink/ComfyUI-Advanced-ControlNet) to apply diffrent weights for each latent index.
- Use 2 controlnet modules for two images with weights reverted.

![image](https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/bcca1070-e4a1-4698-a2af-aadf9723d015)

Workflow: [cn-2images.json](https://github.com/ArtVentureX/comfyui-animatediff/blob/main/workflows/cn-2images.json)

Samples:

<table>
<tr>
<td>
<img src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/e73fc3cd-a590-40a9-8b33-11358b54f0cd">
</td>
<td>
<img src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/96c2ee92-d457-4862-94d3-d675b7fa2d1f">
</td>
</tr>
<tr>
<td>
<img src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/46338853-1ae0-433e-925c-2a41e0382e68">
</td>
<td>
<img src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/707e4ce3-3594-4ff5-9a5f-f9596eb2bcf4">
</td>
</tr>
</table>

#### Using GIF as ControlNet input

Using a GIF (or video, or a list of images) as ControlNet input.

![image](https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/cfeed634-e683-4797-b2fd-dbe0926a449e)

Workflow: [cn-vid2vid.json](https://github.com/ArtVentureX/comfyui-animatediff/blob/main/workflows/cn-vid2vid.json)

Samples:

<table>
<tr>
<td>
<img src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/bf926f52-da97-4fb4-b86a-8b26ef5fab04">
</td>
<td>
<img src="https://github.com/ArtVentureX/comfyui-animatediff/assets/133728487/f6472c8c-9b92-47c2-8f28-638726f21be7">
</td>
</tr>
</table>

## Known Issues

### CUDA error: invalid configuration argument

It's an `xformers` bug accidentally triggered by the way the original AnimateDiff CrossAttention is passed in. The current workaround is to disable xformers with `--disable-xformers` when booting ComfyUI.

### GIF split into multiple scenes

![AnimateDiff_00007_](https://github.com/ArtVentureX/comfyui-animatediff/assets/8894763/e6cd53cb-9878-45da-a58a-a15851882386)

Work around:

- Shorter your prompt and negative prompt
- Reduce resolution. AnimateDiff is trained on 512x512 images so it works best with 512x512 output.
- Disable xformers with `--disable-xformers`

### GIF has Wartermark (especially when using mm_sd_v15)

See: https://github.com/continue-revolution/sd-webui-animatediff/issues/31

Training data used by the authors of the AnimateDiff paper contained Shutterstock watermarks. Since mm_sd_v15 was finetuned on finer, less drastic movement, the motion module attempts to replicate the transparency of that watermark and does not get blurred away like mm_sd_v14. Try other community finetuned modules.
