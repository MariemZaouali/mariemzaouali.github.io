---
layout: post
title: Rapid Application Development with Large Language Models (LLMs)
subtitle: fourth TP
tags: [Transformers, NLP et GenAI]
author: Mariem ZAOUALI
---
You will be implementing a common feature that usually sits behind the API of an image-generating endpoint; **synthetic prompts**.

When creating text-conditioned diffusion models, developers usually create synthetic keyword-rich datasets for training that allow the model to learn strong customization priors. 
- **In an ideal scenario,** an image generator could be prompted to generate a truly-arbitrary high-quality image that perfectly fits any natural-language prompt - as long as the prompt itself is expressive enough.
- **In practice,** image generators are prompted - and sometimes trained - with loose directives and the model makes sprawling assumptions about the details based on its training data. This commonly manifests as "image retrieval," where training data with only minor modifications gets produced.

Most providers would be more interested in giving people the freedom to prompt the model however they want, so many choose to incorporate text-to-text interfaces that map from "regular human prompt" to "diffusion input prompt" space. 

### Step 1: Ingestion
```python

import base64
from pathlib import Path
from IPython.display import display, Image
from langchain_nvidia_ai_endpoints import ChatNVIDIA


def ask_about_image(image_path: str, question: str = "Describe the image") -> str:
    ####################################################################
    ## < EXERCISE SCOPE

    # Display image
    #display(Image(image_path))

    # Encode image to base64
    with open(image_path, "rb") as f:
        image_b64 = base64.b64encode(f.read()).decode()


    vlm = ChatNVIDIA(model="HuggingFaceTB/SmolVLM-Instruct",
                    base_url="http://0.0.0.0:9002/v1",
                    temperature=1)

    # Simple prompt with the actual question parameter
    messages = [("user", [
        {"type": "text", "text": question},
        {"type": "image_url", "image_url": {"url": f"data:image/jpeg;base64,{image_b64}"}}
    ])]
    
    # Single API call - no batching/caching/optimization as suggested
    response = vlm.invoke(messages)
    return response.content

    ## EXERCISE SCOPE >
    ####################################################################



description = ask_about_image("img-files/paint-cat.jpg", "Describe the image")
print("Description:", description)

```
### Step 2 : Image Generation

```python
import torch
from diffusers import DiffusionPipeline
import matplotlib.pyplot as plt
from PIL import Image
import io
import os

## TODO: Implement this method as appropriate
def generate_images(prompt: str, n: int = 1):
    ####################################################################
    ## < EXERCISE SCOPE
    
    # Load the pipeline
    pipe = DiffusionPipeline.from_pretrained(
        "stabilityai/stable-diffusion-xl-base-1.0",
        torch_dtype=torch.float16,
        use_safetensors=True,
        variant="fp16",
    ).to("cuda")
    
    # Generate n images
    images = pipe(prompt=prompt, num_images_per_prompt=n).images
    
    return images
    ## EXERCISE SCOPE >
    ####################################################################

def plot_imgs(images, r=2, c=2, original_image_name="image.png", output_dir="generated_images"):
    """Plot PIL Images and save them to files. Returns list of saved image paths."""
    # Ensure output directory exists
    os.makedirs(output_dir, exist_ok=True)
    
    # Handle single image case
    if not isinstance(images, list):
        images = [images]
    
    fig, axes = plt.subplots(r, c, figsize=(c * 4, r * 4))
    axes = axes.flatten() if hasattr(axes, "flatten") else [axes]
    
    saved_paths = []
    base_name = os.path.splitext(os.path.basename(original_image_name))[0]
    
    for i, ax in enumerate(axes):
        if i < len(images):
            ax.imshow(images[i])
            ax.axis('off')

            # Save image
            file_path = os.path.join(output_dir, f"{base_name}_{i+1}.png")
            images[i].save(file_path)
            saved_paths.append(file_path)
            print(f"Saved: {file_path}")
        else:
            ax.axis('off')

    plt.tight_layout()
    plt.show()
    
    return saved_paths


# Usage example
images = generate_images(description, n=1)
plot_imgs(images, 1, 1)

```

### Prompt synthesis

```python
from langchain_nvidia_ai_endpoints import ChatNVIDIA
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
import re

def llm_rewrite_to_image_prompts(user_query: str, n: int = 4) -> list[str]:
    ####################################################################
    ## < EXERCISE SCOPE
    
    ## TODO: Create a pipeline for synthetic prompts, outputting a string.
    
    #  Update the system prompt to ask for multiple prompts
    prompt = ChatPromptTemplate.from_messages([
        ("system", 
             f"Create {n} distinct and creative Stable Diffusion prompts based on the user's request. "
             "Each prompt should be detailed, visual, and suitable for AI image generation. "
             "Make each prompt unique with different styles, perspectives, or interpretations. "
             "Return exactly {n} prompts as a numbered list (1., 2., 3., 4.)."
        ), 
        ("user", "Create image prompts for: {input}"),
    ])
    
    model = ChatNVIDIA(model="meta/llama-3.3-70b-instruct",
                      base_url="http://0.0.0.0:9004/v1")
    chain = prompt | model | StrOutputParser()
    
    #  Get the response and parse it into multiple prompts
    response = chain.invoke({"input": user_query, "n": n})
    
    # Parse the response to extract individual prompts
    print("Raw response:", response)  # Debug: see what the model returns
    
    # Split the response into lines and extract numbered items
    lines = response.strip().split('\n')
    sd_prompts = []
    
    for line in lines:
        line = line.strip()
        # Look for lines that start with numbers (1., 2., 3., 4.)
        if re.match(r'^\d+[\.\)]\s+', line):
            # Remove the numbering and clean up
            clean_prompt = re.sub(r'^\d+[\.\)]\s+', '', line)
            if clean_prompt and len(clean_prompt) > 5:
                sd_prompts.append(clean_prompt)
    
    #  Ensure we have exactly n prompts
    # If we got fewer, create some fallback variations
    while len(sd_prompts) < n:
        sd_prompts.append(f"{user_query} - artistic variation {len(sd_prompts) + 1}")
    
    # Take only the first n prompts
    sd_prompts = sd_prompts[:n]
    
    assert len(sd_prompts) == n
    return sd_prompts
    
    ## EXERCISE SCOPE >
    ####################################################################

# Test it
new_sd_prompts = llm_rewrite_to_image_prompts(description, n=4)
print("Generated Prompts:")
for i, prompt in enumerate(new_sd_prompts, 1):
    print(f"{i}. {prompt}")
```

### Pipelining and Iterating

```python
## TODO: Execute on assessment objective
def generate_images_from_image(image_url: str, num_images = 4):

    print(f"Generating images for {image_url}")

    ####################################################################
    ## < EXERCISE SCOPE
    print("********************************************STEP1***********************************************\n")
    ## TODO: Generate the description of the image provided in image_url
    original_description = ask_about_image(image_url, "Describe the image")
    print("********************************************STEP2***********************************************\n")
    ## TODO: Generate four disjoint prompts, hopefully different, to feed into SDXL
    new_sd_prompts = llm_rewrite_to_image_prompts(original_description, n=4) 
    print("********************************************STEP3***********************************************\n")
    ## TODO: Generate the resulting images
    images = [generate_images(sd_prompt)[0] for sd_prompt in new_sd_prompts]
    images_paths=plot_imgs(images, r=2, c=2, original_image_name=image_url, output_dir="generated_images")

    
    
    ## EXERCISE SCOPE >
    ####################################################################

    
    return images_paths, new_sd_prompts, original_description

results = []
results += [generate_images_from_image("imgs/agent-overview.png")]
results += [generate_images_from_image("imgs/multimodal.png")]
results += [generate_images_from_image("img-files/tree-frog.jpg")]
results += [generate_images_from_image("img-files/paint-cat.jpg")]

```
To get your NVIDIA certificate, run the cell:
```python

import os
import json
import requests
from PIL import Image
import re

def send_metadata(results):    
    
    save_dir="generated_images"
    
    # Collect all image paths and metadata
    all_metadata = []

    for result in results:
        image_paths, prompts, original_description = result
        
        # Convert any Image objects to string representations
        processed_paths = []
        for path in image_paths:
            if isinstance(path, Image.Image):  # Check if it's a PIL Image object
                processed_paths.append("generated_image")
            else:
                processed_paths.append(str(path).replace("/dli/task/", ""))
        
        # Ensure prompts don't contain any Image objects
        processed_prompts = []
        for prompt in prompts:
            if isinstance(prompt, Image.Image):
                processed_prompts.append("image_prompt")
            else:
                processed_prompts.append(str(prompt))
        
        # Append metadata for the current batch
        all_metadata.append({
            "original_description": str(original_description),  # Ensure this is string too
            "prompts": processed_prompts,
            "image_paths": processed_paths
        })
    
    # Save all metadata in a single JSON file
    metadata_path = os.path.join(save_dir, "all_metadata.json")
    with open(metadata_path, 'w') as f:
        json.dump(all_metadata, f, indent=4)
    return all_metadata

## Generate your submission
submission = send_metadata(results)

## Send the submission over to the assessment runner
response = requests.post(
    "http://docker_router:8070/run_assessment", 
    json={"submission": submission},
)

response.raise_for_status()

try: 
    print(response.json().get("result") or "<No Results>")
    print(response.json().get("messages") or "<No More Messages>")
    print(response.json().get("exceptions") or "<No Exceptions>")
except:
    print(response.__dict__)
```
