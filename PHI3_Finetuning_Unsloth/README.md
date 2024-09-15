# Fine-tuning Microsoft PHI3 with Unsloth for E-Commerce Chatbot Development

```Phi-3```, is a powerful large language model (LLM) from Microsoft AI, but to truly unlock its potential for specific needs, fine-tuning on custom data is crucial.   
We will use ```Unsloth```, a cutting-edge library, to streamline the fine-tuning process of Phi-3 for our unique dataset.

## Why Unsloth ?
1. Faster Training: Unsloth boasts significantly faster training speeds compared to traditional methods like Transformers. This translates to quicker experimentation cycles and reduced training costs.
2. Lower Memory Footprint: Unsloth utilizes efficient memory usage, allowing you to fine-tune Phi-3 even on machines with limited resources.
3. Simplified Workflow: Unsloth provides a user-friendly interface, making fine-tuning accessible even for those without extensive machine learning expertise.

## Step by Step : 

1. Set up Python Environment
   1. Install Necessary Libraries
      ```bash
      !pip install "unsloth[colab-new] @ git+https://github.com/unslothai/unsloth.git"
      !pip install trl peft accelerate bitsandbytes
      !pip install xformers
      ```
    2. Import Necessary Libraries
2. Choose Appropriate ```PHI-3``` variant. (mini, instruct, moderate, large)
3. ```Custom Dataset``` preparation: Can be chosen from HuggingFace, Kaggle, etc., in a format suitable for finetuning.  
   (Structuring data into input-output pairs)
4. Dataset : [dataset](https://huggingface.co/datasets/heliosbrahma/mental_health_chatbot_dataset)

5. Code : -> [Notebook](phi3-finetuning-unsloth.ipynb)
   1. Install Libraries
   2. Import Libraries
   3. Load ```PHI-3-mini-4k-instruct``` model
   4. Set Up FineTuning Parameters
   5. Prepare Training Data, (Format the prompts suitable for fine-tuning)
   6. Fine-Tune with Unsloth
   7. Show current Memory Stats
   8. Train the model
   9. Check trained metrics
   10. Define prompt and Inference with Fine-Tuned model
   11. Save the Fine-Tuned Model

## Tech Stack :
- ```Unsloth```
- ```PHI-3```
- ```HuggingFace```
- ```PEFT```

## References :
 - [https://unsloth.ai/](https://unsloth.ai/)
 - [https://github.com/unslothai/unsloth](https://github.com/unslothai/unsloth)
 - [https://huggingface.co/datasets/qgyd2021/e_commerce_customer_service](https://huggingface.co/datasets/qgyd2021/e_commerce_customer_service)
 - [https://huggingface.co/datasets/heliosbrahma/mental_health_chatbot_dataset](https://huggingface.co/datasets/heliosbrahma/mental_health_chatbot_dataset)
 
