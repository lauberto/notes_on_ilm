# notes_on_ilm
This repository is used to store notes on how ILM works

## START OF TRAINING
1. Device is initialized
2. A training directory is created using “args.train_dir”
3. A tokenizer is created using [line 283](https://github.com/chrisdonahue/ilm/blob/master/train_ilm.py#L283) in train_ilm.py  
```tokenizer = ilm.tokenize.util.Tokenizer[args.tokenizer_name.upper()]```  
This way ```tokenizer``` is set to either GPT2, CUSTOM, etc...
4. New mask tokens are added to the tokenizer. To do this we need the ```vocab_size```. To get it, the encoder must be initialized correctly: update ```vocab_size``` function in ```tokenize_util.py``` (line 170).
5. The encoder (tokenizer) is loaded from the ```OFFICIAL_GPT2_ENCODER_DIR```, which contains ```encoder.json``` (a tokoen to id dictionary), and ```vocab.bpe``` (a file containing the most frequent merges of the tokenizer) 
    * rugpt3xl utilizes a tokenizer which is also based on these files, however they are called respectively ```vocab.json``` and ```merges.txt```
6. Train and eval data are loaded.
7. To compute logits, the model is called on a tensor of **token_ids**. For this reason, the model does not need an embodied tokenizer, as it is in the rugpt3xl original repo. They embody the tokenizer into the model, so that they can generate new text, based on an input text that needs to be tokenized. This is not something that we need to do, so maybe we can just remove the tokenizer from the ```RuGPT3XL``` class object. 

## RUGPT3MODEL INITIALIZATION
1. Tokenizer must be intialized the ilm way, i.e. using the encoder module
2. When ```from_pretrained``` you must set ```model_name_or_path=path/to/rugpt3xl/config/dir```. If you don't want do that, you can still use the hf card ```sberbank-ai/rugpt3xl```, this way the pre-trained model will be downloaded on the go, using ```hf_bucket_url```, then ```cached_path```, which downloads the file from the hf url and stores it as cache.
3.  

## TODO
1. Copy RUGPT3XL ```vocab.json``` and ```merges.txt``` on Google drive, so you can access them from Colab.
2. Make ```RUGPT3XL_finetune_ILM_example.ipynb``` file to test ilm training 

