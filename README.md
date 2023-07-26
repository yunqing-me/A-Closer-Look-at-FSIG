# A Closer Look at Few-shot Image Generation
The IEEE / CVF Computer Vision and Pattern Recognition Conference (CVPR) 2022


<p align='left' style="text-align:left;font-size:1.1em;">
<b>
    [<a href="https://arxiv.org/abs/2205.03805" target="_blank" style="text-decoration: none;">Paper</a>]&nbsp;&nbsp;
    [<a href="https://yunqing-me.github.io/A-Closer-Look-at-FSIG/" target="_blank" style="text-decoration: none;">Project Page</a>]&nbsp;&nbsp;
    [<a href="https://drive.google.com/file/d/1ttXaAqWS8YY3CisvhXscl2PIPD7i1G6O/view?usp=sharing" target="_blank" style="text-decoration: none;">Slides</a>]&nbsp;&nbsp;
    [<a href="https://drive.google.com/file/d/1Ed3UezqoZn7k2Uv4bpep6nK2LveTOZHX/view?usp=sharing" target="_blank" style="text-decoration: none;">Poster</a>]&nbsp;&nbsp;
    [<a href="https://drive.google.com/drive/folders/1GkiYFeUd85nDNsrLG52J-xz-jLjiKED3" target="_blank" style="text-decoration: none;">Data Repository</a>]
    
</b>
</p>

Code/Project page will be actively updated.

### TL, DR

```
In this work, we take a closer look at few-shot image generation (FSIG) problem. Our analysis discovers that: current methods for FSIG achieve similar quality of generated images after few-shot adaptation on target training images, while the main difference is on the diversity of those generated samples. State-of-the-art FSIG algorithms generates visual-pleasant images with both high-quality and high-diversity.

Based on our analysis, we propose a mutual-information based contrastive learning algorithm (DCL) that preserves the diversity of generated images during adaptation. 
```

# Installation and Environment:

- Platform: Linux
- Tesla V100 GPUs / (or A100 GPUs)
- PyTorch 1.7.0
- Python 3.6.9
- lmdb, tqdm

Alternatively, A suitable conda environment named `fsig` can be created and activated with:
```
git clone https://github.com/yunqing-me/A-Closer-Look-at-FSIG.git
conda env create -f environment.yml
conda activate fsig
cd A-Closer-Look-at-FSIG
```

# Prepare datasets

### Step 1. 
Prepare the few-shot training dataset using `lmdb` format

For example, download the 10-shot target set, `Babies` ([Link](https://drive.google.com/file/d/1P8JMLq2Kk61MbEZDgwytqXxfrhG-NqcR/view?usp=sharing)) and `AFHQ-Cat`([Link](https://drive.google.com/file/d/1zgacEE0jiiDxttbK81fk6miY_4Ithhw-/view?usp=sharing)), and organize your directory as follows:

~~~
10-shot-{babies/afhq_cat}
└── images		
    └── image-1.png
    └── image-2.png
    └── ...
    └── image-10.png
~~~

Then, transform to `lmdb` format:

`python prepare_data.py --input_path [your_data_path_of_{babies/afhq_cat}] --output_path ./_processed_train/[your_lmdb_data_path_of_{babies/afhq_cat}]`

### Step 2. 
Prepare the entire target dataset for evaluation

For example, download the entire dataset, `Babies`([Link](https://drive.google.com/file/d/1xBpBRmPRoVXsWerv_zx4kQ4nDQUOsqu_/view?usp=share_link)) and `AFHQ-Cat`([Link](https://drive.google.com/file/d/1_-cDkzqz3LlotXSYMBXZLterSQe4fR7S/view?usp=share_link)), and organize your directory as follows:

~~~
entire-{babies/afhq_cat}
└── images		
    └── image-1.png
    └── image-2.png
    └── ...
    └── image-n.png
~~~

Then, transform to lmdb format for evaluation

`python prepare_data.py --input_path [your_data_path_of_entire_{babies/afhq_cat}] --output_path ./_processed_test/[your_lmdb_data_path_of_entire_{babies/afhq_cat}]`

### Step 3. 
Download the GAN model pretrained on FFHQ from [here](https://drive.google.com/file/d/1TQ_6x74RPQf03mSjtqUijM4MZEMyn7HI/view). Then, save it to `./_pretrained/style_gan_source_ffhq.pt`.

# Bibtex
If you find our work useful in your research, please consider citing our paper:
```
@InProceedings{Zhao_2022_CVPR,
    author    = {Zhao, Yunqing and Ding, Henghui and Huang, Houjing and Cheung, Ngai-Man},
    title     = {A Closer Look at Few-Shot Image Generation},
    booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
    month     = {June},
    year      = {2022},
    pages     = {9140-9150}
}
```