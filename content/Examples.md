# [Optimizing LLMs for Speed and Memory (huggingface.co)](https://huggingface.co/docs/transformers/v4.38.2/en/llm_tutorial_optimization)
```
from transformers import AutoModelForCausalLM, AutoTokenizer, pipeline
import torch

model = AutoModelForCausalLM.from_pretrained("bigcode/octocoder", torch_dtype=torch.bfloat16, device_map="auto", pad_token_id=0)
tokenizer = AutoTokenizer.from_pretrained("bigcode/octocoder")

pipe = pipeline("text-generation", model=model, tokenizer=tokenizer)

prompt = "Question: Please write a function in Python that transforms bytes to Giga bytes.\n\nAnswer:"

result = pipe(prompt, max_new_tokens=60)[0]["generated_text"][len(prompt):]
result
```

# Pipelines
[Pipelines (huggingface.co)](https://huggingface.co/docs/transformers/main_classes/pipelines#transformers.TextGenerationPipeline)
Text generation pipeline

# Installation
```
activate the virtual environment with `source project_env/bin/activate`

  

## Installing pytorch

pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/rocm5.7

pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu

can probably get away without torchaudio or torchvision

  

https://pytorch.org/get-started/locally/

  

## Installation commands

pip install huggingface_hub

pip install transformers

pytorch (initially cpu)
```


# Long Context
[The Secret Sauce behind 100K context window in LLMs: all tricks in one place | by Galina Alperovich | GoPenAI](https://blog.gopenai.com/how-to-speed-up-llms-and-use-100k-context-window-all-tricks-in-one-place-ffd40577b4c)

[Introducing MPT-7B: A New Standard for Open-Source, Commercially Usable LLMs | Databricks Blog](https://www.databricks.com/blog/mpt-7b)

The chat is done using [Templates for Chat Models (huggingface.co)](https://huggingface.co/docs/transformers/main/en/chat_templating)

So either the MPT story writer model or [mistralai/Mixtral-8x7B-Instruct-v0.1 · Hugging Face](https://huggingface.co/mistralai/Mixtral-8x7B-Instruct-v0.1)

Gemma badly hallucinated a bunch of requirements that aren't present.
```
<bos><start_of_turn>user
You are a helpful assistant that writes software specifications. You will take a current version of the specification and a description of a change and combine them into a new specification.Specification: The user can create or edit bookings. Change Request: The user can also delete bookings.<end_of_turn>
<start_of_turn>model
**New Specification:**

The user can create, edit, and delete bookings.

**Features:**

**Booking Creation:**
- User can create new bookings by providing the following information:
    - Name
    - Date
    - Time
    - Duration
    - Number of guests
    - Contact information

**Booking Editing:**
- User can edit existing bookings by modifying the following information:
    - Date
    - Time
    - Duration
    - Number of guests
    - Contact information

**Booking Deletion:**
- User can delete bookings by selecting them and clicking on a "Delete" button.
- Confirmation prompt to ensure user intent before deletion.

**Additional Notes:**

- The system should
```