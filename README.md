# MultiModal BiTransformers (MMBT)

## Introduction

[MMBT](https://arxiv.org/abs/1909.02950) is the accompanying code repository for the paper titled, "Supervised Multimodal Bitransformers for Classifying Images and Text" by Douwe Kiela, Suvrat Bhooshan, Hamed Firooz, Ethan Perez and Davide Testuggine.
 

The goal of the repository is to provide an implementation of the MMBT model and replicate the experiments in the paper.

Paper Link: https://arxiv.org/abs/1909.02950 

 ## Getting Started

### Setup Enviroment

Use environment.yml for creation of virtual environment:

`conda env create --file environment.yml`

Or use mamba instead of conda because it's faster.

### Model Training

train.py provides the common training pipeline for all datasets. 
- **task**: mmimdb, food101, vsnli
- **model**: bow, img, concatbow, bert, concatbert, mmbt

The following paths need to be set to start training.

- **data_path**: Assumes a subfolder for each dataset. 
- **savedir**: Location to save model checkpoints.
- **glove_path**: Path to glove embeds file. Needed for bow, concatbow models.

### Training on MMIMDB

Preparation of dataset:

```
python scripts/mmimdb.py /path/to/mmimdb/parent/folder/
python scripts/test_hard_gt.py --task mmimdb --path /path/to/mmimdb/parent/folder/
```

Baseline training:

```
python -m mmbt.train --batch_sz 4 --gradient_accumulation_steps 40 \
 --savedir /path/to/savedir/ --name mmbt_model_run \
 --data_path /path/to/mmimdb/parent/folder/ \
 --task mmimdb --task_type multilabel \
 --model mmbt --num_image_embeds 3 --freeze_txt 5 --freeze_img 3  \
 --patience 5 --dropout 0.1 --lr 5e-05 --warmup 0.1 --max_epochs 100 --seed 1
```  

 ## License
 
 MMBT is licensed under Creative Commons-Non Commercial 4.0. See the LICENSE file for details.
 
 
## Citation

Please cite it as follows


```
@article{kiela2019supervised,
  title={Supervised Multimodal Bitransformers for Classifying Images and Text},
  author={Kiela, Douwe and Bhooshan, Suvrat and Firooz, Hamed and Testuggine, Davide},
  journal={arXiv preprint arXiv:1909.02950},
  year={2019}
}
```
