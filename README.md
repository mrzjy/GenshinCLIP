# GenshinCLIP
A simple opensourced SigLIP model fine-tuned on Genshin Impact's image-text pairs.

The model is far from being perfect, but could still offer some better text-image matching performance in some Genshin Impact scenarios.

## Model Card

| Model Name                             | Link                                                                               |
|----------------------------------------|------------------------------------------------------------------------------------|
| GenshinImpact-ViT-SO400M-14-SigLIP-384 | [Huggingface](https://huggingface.co/mrzjy/GenshinImpact-ViT-SO400M-14-SigLIP-384) |

## Case Study

Note: Case 4 is bad case.

| Case | Image                                                                                                                                    | Multiple Choices                                                                                                                        | CLIPScore<br/>(After Finetune)                   | CLIPScore<br/>(Before Finetune)                                     |
|------|------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------|---------------------------------------------------------------------|
| 1    | <img src="https://static.wikia.nocookie.net/gensin-impact/images/2/24/Ganyu_Card.png/revision/latest?cb=20230519012433" height="64">     | 1) This is an image of Kuki Shinobu<br/>2) This is an image of Ganyu<br/>3) This is an image of Keqing<br/>4) This is an image of Liyue | 1) 0.000<br>2) **0.438**<br>3) 0.000<br>4) 0.000 | 1) **1.207e-06**<br/>2) 4.144e-08<br/>3) 1.201e-07<br/>4) 2.212e-08 |
| 2    | <img src="https://static.wikia.nocookie.net/gensin-impact/images/3/33/Qingce_Village.png/revision/latest?cb=20220626161951" height="64"> | 1) This is an area of Liyue<br/>2) This is an area of Mondstadt<br/>3) This is an area of Sumeru<br/>4) This is Qingce Village          | 1) 0.016<br>2) 0.000<br>3) 0.001<br>4) **0.233** | 1) 0.015<br/>2) 0.003<br/>3) 0.009<br/>4) **0.377**                 |
| 3    | <img src="https://static.wikia.nocookie.net/gensin-impact/images/0/0c/Enemy_Boreas.png/revision/latest?cb=20210426192800" height="64">   | 1) This is Andrius Wolf of the North<br/>2) This is Stormterror Dvalin<br/>3) This is Guardian of Apep's Oasis                          | 1) 1.000<br>2) 0.000<br>3) 0.000                 | 1) **0.001**<br/>2) 0.000<br/>3) 0.000                              |
| 4    | <img src="https://static.wikia.nocookie.net/gensin-impact/images/0/0c/Enemy_Boreas.png/revision/latest?cb=20210426192800" height="64">   | 1) This is Amakumo Fruit<br/>2) This is Padisarahs<br/>3) This is Naku Weeds                                                            | 1) 1) 0.000<br>2) 0.000<br>3) **0.024**          | 1) 9.425e-07<br/>2) 1.207e-06<br/>3) **1.669e-05**                  |


## Training
### SigLIP for GenshinImpact

[SigLIP model](https://huggingface.co/timm/ViT-SO400M-14-SigLIP-384) further fine-tuned on 15k Genshin Impact English text-image pairs at resolution 384x384.

### Training data description

There're currently 17,428 (train) and 918 (validation) text-image pairs used for model training.

All the images and texts are crawled from [Genshin Fandom Wiki](https://genshin-impact.fandom.com/wiki) and are manually parsed to form text-image pairs.

**Image Processing:**
- Size: Resize all images to 384x384 pixels to match the original model training settings.
- Format: Accept images in PNG or GIF format. For GIFs, extract a random frame to create a static image for text-image pairs.

**Text Processing:**
- Source: Text can be from the simple caption attribute of an HTML `<img>` tag or specified web content.
- Format: Prepend all texts with "Genshin Impact" along with some simple template to form natural language sentences.

The data distribution is as follows:

![data_distribution.png](img%2Fdata_distribution.png)

