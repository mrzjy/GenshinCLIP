# GenshinCLIP
A simple opensourced SigLIP model fine-tuned on Genshin Impact's image-text pairs.

The model is far from being perfect, but could still offer some better model performance in some Genshin Impact scenarios.

## Case Study
| Id | Image                                                                                                                                    | Multiple Choices                                                                                                                        | CLIPScore                                                       |
|----|------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| 1  | <img src="https://static.wikia.nocookie.net/gensin-impact/images/2/24/Ganyu_Card.png/revision/latest?cb=20230519012433" height="96">     | 1) This is an image of Kuki Shinobu<br/>2) This is an image of Ganyu<br/>3) This is an image of Keqing<br/>4) This is an image of Liyue | 1) 5.202e-10<br/>2) **0.438**<br/>3) 2.432e-05<br/>4) 1.276e-07 |
| 2  | <img src="https://static.wikia.nocookie.net/gensin-impact/images/3/33/Qingce_Village.png/revision/latest?cb=20220626161951" height="96"> | 1) This is an area of Liyue<br/>2) This is an area of Mondstadt<br/>3) This is an area of Sumeru<br/>4) This is Qingce Village          | 1) 0.003<br/>2) 6.139e-06<br/>3) 6.628e-05<br/>4) **0.072**     |
| 3  | <img src="https://static.wikia.nocookie.net/gensin-impact/images/0/0c/Enemy_Boreas.png/revision/latest?cb=20210426192800" height="96">   | 1) This is Andrius Wolf of the North<br/>2) This is Stormterror Dvalin<br/>3) This is Guardian of Apep's Oasis                          | 1) **0.996**<br/>2) 1.669e-05<br/>3) 2.783e-10                  |


## Training
### SigLIP for GenshinImpact

[SigLIP model](https://huggingface.co/timm/ViT-SO400M-14-SigLIP-384) fine-tuned on 15k Genshin Impact English text-image pairs at resolution 384x384.

### Training data description

There're currently 15,564 (train) and 820 (validation) text-image pairs used for model training.

All the images and texts are crawled from [Genshin Fandom Wiki](https://genshin-impact.fandom.com/wiki) and are manually parsed to form text-image pairs.

The text could either be a simple caption attribute from html \<img\> tag, or specified text content on the web, together with some simple template to form a natural language (e.g., all texts are prepended with "Genshin Impact\n").


