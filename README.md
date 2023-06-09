# 2023-NYCU-AI-FINAL
# Chinese Article Summarization
## Group Member
何存益 110550165
<br/>
周冠辰 110550089
<br/>
文玠敦 110550032
<br/>
范均宏 110550083
## Report and Presentation
[Team10_Chinese_Text_Summarization.pdf](https://github.com/kevinchou0518/2023-NYCU-AI-Final-Project-Team-10/blob/main/Team10_Chinese_Text_Summarization.pdf)
<br/>
[Presentatioin Video](https://www.youtube.com/watch?v=UFe0m9H5UbE&ab_channel=%E6%96%87%E7%8E%A0%E6%95%A6)
###  Download PyTorch version
```
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```
### Setup playground
```
pip install -r requirements.txt
```
## Target: Doing Chinese article summarization with two different methods
 1.Extractive Method
<br/>
 2.Abstractive Method

## Dataset
Web crawling the news in [ETtoday](https://www.ettoday.net/?from=logo)
<br/>
Detail in [build_dataset.py](https://github.com/kevinchou0518/2023-NYCU-AI-Final-Project-Team-10/blob/main/build_dataset.py)
## Baseline: Extractive Method - Sentence Scoring Method
Implementation:
<br/>
1.Tokenize the sentence
<br/>
2.Get the high frequency words
<br/>
3.Score the sentence
<br/>
4.Article summarize
<br/>
Detail in [extrative_method.py](https://github.com/kevinchou0518/2023-NYCU-AI-Final-Project-Team-10/blob/main/extrative_method.py)
## Main Approach: Abstractive Method - Fine-tuning mt5-model
Using pre-train transformer model mt5 provided by google 
<br/>
Fine-tuning the mt5-model with our collected dataset 
<br/>
### Hyperparameters
batch size: 4
<br/>
accumulate steps: 16
<br/>
epoch: 5
<br/>
learning rate: 5e-5
<br/>
optimizer: Adafactor with weight decay = 1e-2
<br/>
scheduler: Linear decay with warm up steps = 90
<br/>
Detail in [new_train.py](https://github.com/kevinchou0518/2023-NYCU-AI-Final-Project-Team-10/blob/main/new_train.py) train()
## Further Approach: Apply Reinforcement Learning on Fine-tuning mt5-model
Use ROUGE scores to calculate reward
<br/>
Same paramter in Main Approach
<br/>
Detail in [new_train.py](https://github.com/kevinchou0518/2023-NYCU-AI-Final-Project-Team-10/blob/main/new_train.py) rl_train()
## Evaluating the result
Using ROUGE which is the most used package designed for automatic summarization
<br/>
| Methods        | ROUGE-1           | ROUGE-2  | ROUGE-L |
| ------------- |:-------------:|:-------------:|:-------------:|
| sentence scoring method | 0.246016 | 0.105189 | 0.214126 |
| mt5 model without fine-tuning | 0.140646 | 0.064830 | 0.138213 |
| Supervised Learning | 0.389000 | 0.194737 | 0.343403 |
| Supervised Learning | 0.400387 | 0.198889 | 0.345834 |
## Download the model we trained
[Model we trained](https://drive.google.com/drive/folders/1E4AF4g4bfSdKDP1-oltmRTshePP5uszq?usp=drive_link)
## Related Paper
1.[Exploring the Limits of Transfer Learning with a Unified Text-to-Text Transformer](https://jmlr.org/papers/volume21/20-074/20-074.pdf)
<br/>
2.[Attention Is All You Need](https://arxiv.org/pdf/1706.03762.pdf)
<br/>
3.[mT5: A Massively Multilingual Pre-trained Text-to-Text Transformer](https://arxiv.org/pdf/2010.11934.pdf)
<br/>
4.[A DEEP REINFORCED MODEL FOR ABSTRACTIVE SUMMARIZATION](https://arxiv.org/pdf/1705.04304.pdf)
## Related website
1.[ETtoday](https://www.ettoday.net)
<br/>
2.[ckiptagger](https://github.com/ckiplab/ckiptagger)
<br/>
3.[Huggingface mt5 model](https://huggingface.co/docs/transformers/model_doc/mt5)
