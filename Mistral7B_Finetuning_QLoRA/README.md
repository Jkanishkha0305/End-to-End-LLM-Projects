# Mistral-7B : Finetuning step by step with custom dataset using PEFT and Low Rank Adaptation

## Step-by-Step : 
1. ```Dataset``` : We will be working on a healthcare dataset that contains about 110K+ rows of patient’s queries and the doctor’s opinions. For experimentation used around 5000 randomly sampled rows from this dataset.
So this is what the dataset looks like, 90% is being used for train and 10% is being used for eval.

2. ```Format Prompts``` : The structure of the data contains instructions, input and output column. We have to format them in certain manner in order to fee dto the LLM. Since LLMS are fancy Transformer decoders, combine everything in certain format, tokenize and give it to the model. 

3. ```Tokeizing``` : We can tokenize the dataset using ```HuggingFace's AutoTokenizer```.  
   Note : We have used the padding token as eos_token which is end of sequence token and padding style is left so basically padding tokens will be added at the beginning of the sequence rather than in the end, why do we do that is because in decoder only architecture the output is a continuation of the input prompt — there would be gaps in the output without left padding.

4. ```Quantized low rank adaptation (QLoRA)``` : To initialize the Mistral-7B Model using Quantized low rank adaptation (QLoRA) :
   ```python
    import torch
    from transformers import AutoTokenizer, AutoModelForCausalLM, BitsAndBytesConfig
    
    base_model_id = "mistralai/Mistral-7B-v0.1"
    bnb_config = BitsAndBytesConfig(
        load_in_4bit=True,
        bnb_4bit_use_double_quant=True,
        bnb_4bit_quant_type="nf4",
        bnb_4bit_compute_dtype=torch.bfloat16
    )
    
    model = AutoModelForCausalLM.from_pretrained(base_model_id, quantization_config=bnb_config, resume_download=True)
   ```
   To understand more about 4-bit Quantization : [Blog](https://huggingface.co/blog/4bit-transformers-bitsandbytes)
   
   We are quantizing and loading the model in 4-bit mode that drastically reduces the memory footprint of   the       model without changing the performance!

6. ```PEFT & LoRA Config``` : PEFT is Parameter Efficient Fine-tuning, its a technique that allows us to freeze most of the model params and tries to train a small percentage of the model params it supports low data scenarios to efficiently finetune the LLM on your domain dataset.  
   To understand more about PEFT : [Blog](https://huggingface.co/blog/peft)

     Find and examine the layers of the Model, Apply ```QLoRA``` to all the linear layers of the model.  
     Those layers are ```q_proj```, ```k_proj```, ```v_proj```, ```o_proj```, ```gate_proj```, ```up_proj```, ```down_proj```, and ```lm_head```.
   
    ```r``` is the rank of the low-rank matrix used in the adapters, which thus controls the number of parameters trained. A higher rank will allow for more expressivity, but there is a compute tradeoff.
    
    ```alpha``` is the scaling factor for the learned weights. The weight matrix is scaled by ```alpha/r```, and thus a higher value for alpha assigns more weight to the LoRA activations.
   
    The values used in the QLoRA paper were ```r=64``` and ```lora_alpha=16```, and these are said to generalize well.  

   Out of 3.8 billion parameters 0.08 are trainable!  

7. ```Training the model``` :
   ```python
    import transformers
    from datetime import datetime
    
    project = "chat-doctor-finetune"
    base_model_name = "mistral"
    run_name = base_model_name + "-" + project
    output_dir = "./" + run_name
    
    trainer = transformers.Trainer(
        model=model,
        train_dataset=tokenized_train_dataset,
        eval_dataset=tokenized_val_dataset,
        args=transformers.TrainingArguments(
            output_dir=output_dir,
            warmup_steps=1,
            per_device_train_batch_size=4,
            gradient_accumulation_steps=1,
            gradient_checkpointing=True,
            max_steps=500,
            learning_rate=2.5e-4, # Want a small lr for finetuning
            #bf16=True,
            optim="paged_adamw_8bit",
            logging_steps=25,              # When to start reporting loss
            logging_dir="./logs",        # Directory for storing logs
            save_strategy="steps",       # Save the model checkpoint every logging step
            save_steps=25,                # Save checkpoints every 50 steps
            evaluation_strategy="steps", # Evaluate the model every logging step
            eval_steps=25,               # Evaluate and save checkpoints every 50 steps
            do_eval=True,                # Perform evaluation at the end of training
        ),
        data_collator=transformers.DataCollatorForLanguageModeling(tokenizer, mlm=False),
    )
    
    model.config.use_cache = False  # silence the warnings. Please re-enable for inference!
    trainer.train(resume_from_checkpoint=True)
   ```
Note : These saves are not the model weights but rather the QLoRA adaptor saved weights, you have to combine these weights with the original model to generate responses!

8. ```Results``` :
   1. First load the Base model.
   2. Now comine the base model with trained saved adaptor weights.

9. ```Gradio App``` : Gradio to create a simple UI endpoint for the model. ```demo.launch()``` to launch the gradio app.  
