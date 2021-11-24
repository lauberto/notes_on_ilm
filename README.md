# notes_on_ilm
This repository is used to store notes on how ILM works

## START OF TRAINING
1. Device is initialized
2. A training directory is created using “args.train_dir”
3. A tokenizer is created using {line 283}[https://github.com/chrisdonahue/ilm/blob/master/train_ilm.py#L283] in train_ilm.py
```tokenizer = ilm.tokenize.util.Tokenizer[args.tokenizer_name.upper()]``` 
This way a 
