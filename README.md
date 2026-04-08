# Flight Price Predicton
An application that predict the cheapest flight price so that user can save more budget for other travel expense.

# 0_Setup
## Resources
1. Install this github repository in your local device.
2. Make sure to change file structure as such:

```
Downloads/
└── FlightPricePrediction/
    ├── 0_Setup/
    |   └──requirements.txt
    ├── 1_Data/
    │   └── Clean_Dataset.csv
    ├── 2_Model/
    |   ├── Classifier
    |   |   ├── LightGBMClassifier.ipynb
    |   |   └── RandomForestClassifier.ipynb
    |   └── Regressor
    |       ├── LightGBMRegressor.ipynb
    |       └── RandomForestRegressor.ipynb
    └── README.md
```

## Virtual Envitronment Setup
1. Install Anaconda ```https://www.anaconda.com/download```
2. Then, create an virtual environment, ```conda create -n FlightPricePrediction python=3.10```
3. Then, activate the environment, ```conda activate FlightPricePrediction```

## Kernel Setup
1. Then, install all dependency, ```pip install -r C:/Users/User/Downloads/FlightPricePrediction/0_Setup/requirements.txt```
2. Then, create an external kernel, ```python -m ipykernel install --user --name=ImageCaption --display-name "ImageCaption"```
3. Open ```C:\Users\User\Downloads\ImageCaption\2_Model\LSTM\ImageCaption30K_LSTM.ipynb``` as Jupyter Notebook and then select "ImageCaption" kernel

In case need to add/update the external kernel:
1. Open Anancoda Prompt
2. Then, activate the environment, ```conda activate ImageCaption```
3. Then, add/modify using ```pip install``` or ```pip uninstall```
4. Restart kernel in Jupyter Notebook

In case need to remove the external kernel:
1. Open Anancoda Prompt
2. To check available kernel to delete, ```jupyter kernelspec list```
3. To remove kernel from Jupyter Notebook, ```jupyter kernelspec uninstall imagecaption```
4. For clean up, remove the entire folder, ```C:\Users\User\anaconda3\envs\ImageCaption``` or ```conda remove --name ImageCaption --all```


# 1_Data
1. Flickr30k dataset (https://www.kaggle.com/datasets/hsankesara/flickr-image-dataset) for medium-sized image captioning
2. GloVe: Global Vectors for Word Representation (https://nlp.stanford.edu/projects/glove/) for LSTM embedding purpose

# 2_Model
## Data Cleaning
- Image Augmentation
- Remove unnecessary string on a caption
- Remove extreme short and long caption

## EDA
### LSTM
#### Dataset
![Screenshot](./Screenshots/Dataset_LSTM.png)

#### Caption Length
![Screenshot](./Screenshots/CaptionLength_LSTM.png)

#### Word Occurrences
![Screenshot](./Screenshots/WordOccurrences_LSTM.png)

### Transformer
#### Dataset
![Screenshot](./Screenshots/Dataset_Transformer.png)

#### Caption Length
![Screenshot](./Screenshots/CaptionLength_Transformer.png)

#### Word Occurrences
![Screenshot](./Screenshots/WordOccurrences_Transformer.png)

## Data Splitting
|  | LSTM | Transformer |
| :---: | :---: | :---: |
| Train | 75% | 78% |
| Validation | 15% | 20% |
| Test | 10% | 2% |

## Build
### LSTM
- LSTM is the baseline and the simplest model to explore.
- Using EfficientNet convolutional neural network (CNN) on LSTM with InceptionV3 as input using image features and embedding with GLove Dataset.

### Transformer
- Transfomer has stated a better result compare to LSTM, so I explore it after LSTM.
- Using EfficientNet convolutional neural network (CNN) on decoded and encoded image with positional embedding.

## Performance
### LSTM
#### Training
At Final Epoch 45/100:
- Training loss: 3.4252
- Validation loss: 3.5931

![Screenshot](./Screenshots/Training_LSTM.png)

#### Result
![Screenshot](./Screenshots/Result1_LSTM.png)

![Screenshot](./Screenshots/Result2_LSTM.png)

Cons:
- Consume more time on image extraction and training
- The lowest accuracy (2%)
- Bad at single and multiple word learning

Pros:
- The loss is low (3.5)
- Better generalization with some fine tuning on label smoothing, image augmentation, embedding, learning rate, dense layer and dropout.

### Transformer
#### Training
At Final Epoch 9/30:
- Training loss: 13.2212 
- Training accuracy: 0.4367
- Validation loss: 13.5932 
- Validation Accuracy: 0.4087

![Screenshot](./Screenshots/Training_Transformer.png)

#### Result
![Screenshot](./Screenshots/Result1_Transformer.png)

![Screenshot](./Screenshots/Result2_Transformer.png)

Cons:
- Bad at multiple word learning
- The loss is higher than LSTM (13.5)

Pros:
- Better at single word learning compare to LSTM
- Consume lesser time on image encode and decode and training time is shorter compare to LSTM
- Better accuracy than LSTM (40%)
- Better generalization with some fine tuning on label smoothing, image augmentation, embedding, learning rate, dense layer and dropout.

