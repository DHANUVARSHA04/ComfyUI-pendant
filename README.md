# ComfyUI-pendant
A ComfyUI project for generating virtual try-on images for accessories like pendants. This workflow takes a product image and seamlessly integrates it onto an AI-generated model.

<img width="2048" height="1368" alt="ComfyUI_00001_hvdua_1753199536" src="https://github.com/user-attachments/assets/99e92487-8f0a-49a2-927b-d922c0010e4f" />
<img width="2048" height="1496" alt="ComfyUI_00001_elvtd_1752657454" src="https://github.com/user-attachments/assets/1a25ab0b-99c6-48dd-94ba-dab7d5f9ef0b" />

## Workflow Overview

This repository contains a `workflow.json` file that defines a complete pipeline for creating photorealistic product placement images. The process is as follows:

1.  **Input:** The workflow begins with a `LoadImage` node where you provide an image of the accessory (e.g., a pendant on a plain background).
2.  **Segmentation:** The accessory is automatically isolated from its background using a `BiRefNet_Hugo` node.
3.  **Scene Preparation:** The canvas is expanded and a mask is created to define the area for inpainting using `TTP_Expand_And_Mask`.
4.  **Prompting:** Detailed positive and negative prompts are constructed using `easy prompt` nodes to describe the desired output, including the model's appearance, clothing, and setting.
5.  **Inpainting:** A powerful FLUX.1-based ControlNet model (`alimama_FLUX.1-dev-Controlnet-Inpainting-Beta.safetensors`) is used to generate a model wearing the accessory within the masked area. The `IC_TRY_ON` LoRA enhances the virtual try-on effect.
6.  **Output:** The final output is a high-quality image of a model realistically wearing the accessory, suitable for advertising or e-commerce.

## Requirements

To use this workflow, you will need a working installation of ComfyUI and several custom nodes and models.

### Custom Nodes

You will need to install the following custom nodes, for example by using the [ComfyUI Manager](https://github.com/ltdrdata/ComfyUI-Manager):

-   `ComfyUI-easy-use`
-   `ComfyUI_hugo_tricks`
-   `TinyterraNodes`
-   `ComfyUI-rgthree-custom-nodes`
-   `ComfyUI-Comfyroll-CustomNodes`
-   `ComfyUI-pysssss`
-   Other common utility nodes for image manipulation (`ImageResize+`, `ImageCrop+`).

### Models

Download the following models and place them in the appropriate subdirectories within your ComfyUI `models` folder:

-   **UNet:** `flux1-dev-fp8-Kijai.safetensors`
-   **VAE:** `ae.sft`
-   **CLIP:** `sd3/t5xxl_fp16.safetensors`, `sd3/clip_l.safetensors`
-   **ControlNet:** `alimama_FLUX.1-dev-Controlnet-Inpainting-Beta.safetensors`
-   **LoRAs:**
    -   `IC_TRY_ON_v3_e4.safetensors`
    -   `Phlux-photorealism-flux.safetensors`

## Usage

1.  Ensure ComfyUI and all required custom nodes are installed.
2.  Ensure all required models are downloaded and correctly placed in your `ComfyUI/models/` directory.
3.  Load the `workflow.json` file from this repository by dragging and dropping it onto the ComfyUI canvas.
4.  In the `LoadImage` node, select the image of the accessory you wish to use.
5.  Adjust the text in the `easy prompt` nodes to customize the model, background, and style.
6.  Click **Queue Prompt** to run the workflow and generate your image.
