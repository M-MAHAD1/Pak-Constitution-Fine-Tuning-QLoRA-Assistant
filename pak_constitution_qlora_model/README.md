---
library_name: peft
tags:
- qlora
- pakistan-constitution
- legal-ai
- lora
- fine-tuning
- llama-3
license: apache-2.0
language:
- en
metrics:
- loss
- perplexity
base_model:
- unsloth/llama-3-8b-Instruct-bnb-4bit
pipeline_tag: text-generation
---

# Pak Constitution QLoRA Assistant

This repository contains the fine-tuned QLoRA adapter weights for an 8-billion parameter legal assistant model based on **Llama-3-8B-Instruct**, adapted specifically for the **Constitution of the Islamic Republic of Pakistan**[cite: 1].

## Model Details

### Model Description

This model is a parameter-efficient fine-tuned (PEFT) causal language model designed to assist researchers, law students, and legal professionals in querying, retrieving, and understanding specific provisions, articles, and chapters of the Constitution of the Islamic Republic of Pakistan[cite: 1].

- **Developed by:** Muhammad Mahad (MMahad01)
- **Funded by [optional]:** Self-funded Academic Final Year Project
- **Shared by [optional]:** Muhammad Mahad
- **Model type:** Causal Language Model (QLoRA Fine-tuned PEFT Adapter)
- **Language(s) (NLP):** English
- **License:** apache-2.0
- **Finetuned from model:** unsloth/llama-3-8b-Instruct-bnb-4bit

### Model Sources

- **Repository:** https://huggingface.co/MMahad01/pak-constitution-qlora-assistant
- **Paper [optional]:** N/A
- **Demo [optional]:** Deployed on Hugging Face Spaces

## Uses

### Direct Use

The model can be used directly for text generation, answering constitutional queries, and explaining legal provisions of Pakistan using official statutory terminology.

### Downstream Use [optional]

Can be integrated into larger legal RAG (Retrieval-Augmented Generation) pipelines, such as the Pak Justice AI Assistant project, to provide localized legal context.

### Out-of-Scope Use

The model is intended for educational, research, and legal assistance purposes. It should not be used as a definitive substitute for formal legal counsel, formal litigation drafting, or professional judicial advice.

## Bias, Risks, and Limitations

The model is trained strictly on statutory text from the Constitution of Pakistan[cite: 1]. While it captures formal legal terminology accurately, generative outputs may occasionally require verification against official legal documents.

### Recommendations

Users (both direct and downstream) should be made aware of the risks, biases, and statutory limitations of language models. All critical legal interpretations should be cross-checked with official gazetted copies of the Constitution.

## How to Get Started with the Model

Use the code below to get started with the model using `transformers` and `peft`:

```python
from transformers import AutoModelForCausalLM, AutoTokenizer
from peft import PeftModel
import torch

base_model_id = "unsloth/llama-3-8b-Instruct-bnb-4bit"
adapter_path = "MMahad01/pak-constitution-qlora-assistant"

tokenizer = AutoTokenizer.from_pretrained(base_model_id)
base_model = AutoModelForCausalLM.from_pretrained(
    base_model_id,
    torch_dtype=torch.bfloat16,
    device_map="auto"
)
model = PeftModel.from_pretrained(base_model, adapter_path)
Training DetailsTraining DataDataset Source: Official legal text extracted from the PDF of THE CONSTITUTION OF THE ISLAMIC REPUBLIC OF PAKISTAN.   Format: Structured into JSONL instruction-input-output pairs (instruction, input, output) segmented by constitutional articles.Training ProcedurePreprocessing [optional]Raw text was extracted using pypdf, segmented by article headings, cleaned of formatting artifacts, and mapped into instruction-tuning samples.Training HyperparametersTraining regime: QLoRA 4-bit NormalFloat (NF4) with BFloat16 mixed precision (bf16=True)LoRA Rank ($r$): 8LoRA Alpha ($\alpha$): 16Target Modules: q_proj, k_proj, v_proj, o_projPer-Device Batch Size: 1Gradient Accumulation Steps: 8Learning Rate: $2 \times 10^{-4}$Epochs: 1Max Sequence Length: 128Speeds, Sizes, Times [optional]Adapter File Size: ~27 MB (Extremely lightweight compared to full model weights)Training Time: Completed efficiently on a single Google Colab free-tier T4 GPU session.EvaluationTesting Data, Factors & MetricsTesting DataEvaluated against a custom benchmark suite consisting of 10 key constitutional articles covering fundamental rights, the judiciary, and the parliament.   FactorsEvaluated across legal domain accuracy, constitutional terminology adherence, and response coherence.MetricsCross-Entropy Loss: Monitored across steps (reduced from initial 2.086 to final 1.620).Perplexity: Tracked via exponential decay to measure text predictability and fluency.ResultsSummaryThe model successfully converged with stable loss reduction, demonstrating a strong grasp of Pakistani constitutional law terms (e.g., Majlis-e-Shoora, Federal Legislative List).Model Examination [optional]Qualitative evaluation confirmed that the model generates formal statutory explanations aligned with the legal framework of the Constitution.   Environmental ImpactCarbon emissions can be estimated using the Machine Learning Impact calculator presented in Lacoste et al. (2019).Hardware Type: NVIDIA T4 GPU (15 GB VRAM)Hours used: ~0.5 hoursCloud Provider: Google ColabCompute Region: Cloud Hosted (US/Europe datacenters)Carbon Emitted: Minimal / Low-power cloud instance trainingTechnical Specifications [optional]Model Architecture and ObjectiveArchitecture: Llama-3-8B-Instruct with bitsandbytes 4-bit quantization and PEFT LoRA layers.Objective: Causal Language Modeling for domain adaptation on legal corpus.Compute InfrastructureHardwareGoogle Colab Free Tier (NVIDIA T4 GPU)SoftwarePython, PyTorch, Hugging Face transformers, peft, trl, bitsandbytes, and accelerate.
@misc{mahad2026pakconstitutionqlora,
  author = {Muhammad Mahad},
  title = {Pak Constitution QLoRA Assistant},
  year = {2026},
  publisher = {Hugging Face Hub},
  journal = {Hugging Face Repository},
  howpublished = {\url{[https://huggingface.co/MMahad01/pak-constitution-qlora-assistant](https://huggingface.co/MMahad01/pak-constitution-qlora-assistant)}}
}
