# Investigating the Impact of Using Image Processing Techniques in Chest X-Ray images for COVID-19 Diagnosis via Deep Learning


## Authors

- [Breno Maurício de Freitas Viana](https://github.com/brenov) (11920060)
- [Felipe Antunes Quirino](https://github.com/felipeaq) (12448645)


## Introduction

Since World Health Organization (WHO) recognized COVID-19 as a global threat, several works of different areas about the topic emerged.
Regarding abnormalities detection, numerous works try to classify COVID-19 cases from Chest X-Ray images and images of other lung image acquisition methods.
Most of these works applied Deep Learning (DL) techniques for predicting COVID-19 and non-COVID-19 cases in the original lung images.


## Objective

This work intends to investigate the impact of using image preprocessing techniques on the chest X-ray images in their classification in COVID-19 and non-COVID-19 cases.
We believe that such a process may improve the COVID-19 diagnosis performed by the ResNet-50 with the original chest X-ray images.
The ResNet-50 version of the ResNet model contains 48 Convolution layers, 1 MaxPool, and 1 Average Pool layer.


## Dataset

In this investigation, we are using the COVID-19 Chest X-ray Database from [Kaggle](https://www.kaggle.com/tawsifurrahman/covid19-radiography-database)
(the dataset present in this repository ([Dataset](Dataset)) present 40 images and it is just a small subset of the COVID-19 Chest X-ray Database).
Furthermore, it was originally provided by Chowdhury et al. [1] and Rahman et al. [2].
This dataset contains chest X-ray images of healthy people (10,192) and people diagnosed with COVID-19, viral pneumonia (1,345), and lung opacity, i.e., non-COVID-19 lung infection (6,012).
All the images are in PNG file format, and their resolution is 299x299 pixels.
The following images present examples of such cases:

<table>
  <tr>
    <td>
      <img src=".github/Normal.png" alt="1" width=250px height=250px>
    </td>
    <td>
      <img src=".github/Lung_Opacity.png" alt="2" width=250px height=250px>
    </td>
   </tr>
   <tr>
      <td>Normal</td>
      <td>Lung Opacity</td>
   </tr>
   <tr>
    <td>
      <img src=".github/Viral_Pneumonia.png" alt="3" width=250px height=250px>
    </td>
    <td>
      <img src=".github/COVID.png" alt="4" width=250px height=250px>
    </td>
   </tr>
   <tr>
      <td>Viral Pneumonia</td>
      <td>COVID-19</td>
  </tr>
</table>


## Methodology

To carry out our investigation, we first perform data augmentation by using the following image processing techniques: noise insertion, rotation, contrast adjustment, and sharpness enhancement.
These image processing methods are implemented in the [augmentation.py](augmentation.py) file.
The data augmentation is performed by the script [augmentate.py](augmentate.py).
This script automatizes the data augmentation process by reading all the images from [Dataset](Dataset) and creating five new versions of each original image: noisy image, 15 degrees rotated image, -15 degrees rotated image, image with contrast adjusted, and image with sharpness enhancement.
We opt for 15-degree and -15-degree rotations to simulate and maybe fix some badly positioned chest X-rays.

After the data augmentation, we used both the original images (from [Dataset](Dataset)) and the images generated by the data augmentation techniques (from [Augmented](Augmented)) for training the ResNet-50.
The CNN model and its training results are present in [Jupyter Notebook file](resnet-50-2.ipynb).
In the next step of this wotk, we will perform the fine-tuning of the ResNet-50 model.


## Partial Results

The partial results are present in [Jupyter Notebook file](resnet-50-2.ipynb) in the folder [Augmented](Augmented).
First, at this point of the project does not make much sense present results in terms of, for instance, accuracy since we trained the model with a small number of images.
Therefore, in the last cell of [Jupyter Notebook file](resnet-50-2.ipynb), we present the result of the ResNet-50 training with images from both [Dataset](Dataset) and [Augmented](Augmented) folders.
Second, the folder [Augmented](Augmented) presents the augmented images generated from the [Dataset](Dataset).
So far, we geneated a total of 200 images.
The following images present some results of the data augmentation process.

<table>
  <tr>
    <td>
      <img src="Dataset/Train/COVID/COVID-1.png" alt="1" width=250px height=250px>
    </td>
    <td>
      <img src="Augmented/Train/COVID/COVID-1_noisy.png" alt="2" width=250px height=250px>
    </td>
    <td>
      <img src="Augmented/Train/COVID/COVID-1_15rotated.png" alt="3" width=250px height=250px>
    </td>
  </tr>
  <tr>
    <td><b>Input image</b></td>
    <td>Noisy image</td>
    <td>15-degree rotated image</td>
  </tr>
  <tr>
    <td>
      <img src="Augmented/Train/COVID/COVID-1_-15rotated.png" alt="1" width=250px height=250px>
    </td>
    <td>
      <img src="Augmented/Train/COVID/COVID-1_contrast.png" alt="2" width=250px height=250px>
    </td>
    <td>
      <img src="Augmented/Train/COVID/COVID-1_sharpness.png" alt="3" width=250px height=250px>
    </td>
  </tr>
  <tr>
    <td>-15-degree rotated image</td>
    <td>Image with contrast adjusted</td>
    <td>Image with sharpeness enhanced</td>
  </tr>
</table>


## References

[1] M.E.H. Chowdhury, T. Rahman, A. Khandakar, R. Mazhar, M.A. Kadir, Z.B. Mahbub, K.R. Islam, M.S. Khan, A. Iqbal, N. Al-Emadi, M.B.I. Reaz, M. T. Islam, “Can AI help in screening Viral and COVID-19 pneumonia?” IEEE Access, Vol. 8, 2020, pp. 132665 - 132676. Paper DOI: (https://doi.org/10.1109/ACCESS.2020.3010287).

[2] Rahman, T., Khandakar, A., Qiblawey, Y., Tahir, A., Kiranyaz, S., Kashem, S.B.A., Islam, M.T., Maadeed, S.A., Zughaier, S.M., Khan, M.S. and Chowdhury, M.E., 2020. Exploring the Effect of Image Enhancement Techniques on COVID-19 Detection using Chest X-ray Images. Paper DOI: (https://doi.org/10.1016/j.compbiomed.2021.104319).
