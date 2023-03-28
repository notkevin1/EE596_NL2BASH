---
license: apache-2.0
tags:
- generated_from_trainer
metrics: 
- nl2bash_m
model-index:
- name: t5-small-finetuned-English-to-BASH
  results: [0.62]
---

# t5-small-finetuned-English-to-BASH

Created by: [Josh Shih](https://huggingface.co/Josh98), [Alex Sha](https://huggingface.co/alexsha), [Kevin Um](https://huggingface.co/kevinum) for EEP 596 - Natural Language Processing at University of Washington (Seattle).

## Model description
This model is a fine-tuned version of [t5-small](https://huggingface.co/t5-small) on a more balanced iteration of the [NL2BASH](https://github.com/TellinaTool/nl2bash/tree/master/data) dataset.
It achieves the following results on the evaluation set:
- Loss: 0.9614
- [nl2bash_m](https://huggingface.co/spaces/Josh98/nl2bash_m): 0.6192
- Gen Len: 14.1044

## Intended uses & limitations
Purpose: To generate bash commands from text input, and help people learn to use linux bash. This is a proof of concept model using transfer learning to fine-tune an existing language model and produce structured code instead of natural language. 

## Training and evaluation data

This model was trained and evaluated using a custom iteration of [NL2BASH](https://github.com/TellinaTool/nl2bash/tree/master/data). The original NL2BASH dataset contains a large class imbalance with too many bash commands which begin with 'find'. 

A maximum threshold was set to remove text/BASH pairs which exceeded the threshold, and [GPT-3](https://openai.com/blog/gpt-3-apps/) API was used to generate text/BASH pairs for those below the threshold.

~5500 original text/BASH pairs and ~5700 generated text/BASH pairs were used, giving a total of ~11200 lines of text/BASH pairs. Shown below is the class distribution for the top-5 commands.
![class_balanced.png](https://s3.amazonaws.com/moonup/production/uploads/1677215336540-63d8b9876ac3104e50cd9634.png)

## Training procedure

### Training hyperparameters

The following hyperparameters were used during training:
- learning_rate: 0.0001
- train_batch_size: 16
- eval_batch_size: 16
- seed: 42
- optimizer: Adam with betas=(0.9,0.999) and epsilon=1e-08
- lr_scheduler_type: linear
- num_epochs: 10

### Training results

| Training Loss | Epoch | Step | Validation Loss | nl2bash_m   | Gen Len |
|:-------------:|:-----:|:----:|:---------------:|:------:|:-------:|
| 1.1451        | 1.0   | 561  | 1.3121          | 0.5184 | 13.7475 |
| 1.4064        | 2.0   | 1122 | 1.1756          | 0.5274 | 14.0812 |
| 1.3184        | 3.0   | 1683 | 1.1131          | 0.5618 | 13.8323 |
| 1.2566        | 4.0   | 2244 | 1.0675          | 0.5811 | 13.9099 |
| 1.195         | 5.0   | 2805 | 1.0312          | 0.5945 | 14.1124 |
| 1.1459        | 6.0   | 3366 | 1.0064          | 0.6057 | 14.0116 |
| 1.092         | 7.0   | 3927 | 0.9854          | 0.6094 | 14.0731 |
| 1.0729        | 8.0   | 4488 | 0.9699          | 0.6159 | 14.1427 |
| 1.037         | 9.0   | 5049 | 0.9650          | 0.6177 | 14.0455 |
| 1.0259        | 10.0  | 5610 | 0.9614          | 0.6192 | 14.1044 |


### Framework versions

- Transformers 4.27.0.dev0
- Pytorch 1.13.1+cu116
- Datasets 2.10.0
- Tokenizers 0.13.2
