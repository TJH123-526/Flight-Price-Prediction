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
    ├── README.md
    └── Screenshots
            ├── LGBMC.png
            ├── LGBMR.png
            ├── Report.png
            ├── RFC.png
            └── RFR.png
```

## Virtual Envitronment Setup
1. Install Anaconda ```https://www.anaconda.com/download```
2. Then, create an virtual environment, ```conda create -n FlightPricePrediction python=3.10```
3. Then, activate the environment, ```conda activate FlightPricePrediction```

## Kernel Setup
1. Then, install all dependency, ```pip install -r C:/Users/User/Downloads/FlightPricePrediction/0_Setup/requirements.txt```
2. Then, create an external kernel, ```python -m ipykernel install --user --name=FlightPricePrediction --display-name "FlightPricePrediction"```
3. Open ```C:\Users\User\Downloads\FlightPricePrediction\2_Model\Regressor\RandomForestRegressor.ipynb``` as Jupyter Notebook and then select "FlightPricePrediction" kernel

In case need to add/update the external kernel:
1. Open Anancoda Prompt
2. Then, activate the environment, ```conda activate FlightPricePrediction```
3. Then, add/modify using ```pip install``` or ```pip uninstall```
4. Restart kernel in Jupyter Notebook

In case need to remove the external kernel:
1. Open Anancoda Prompt
2. To check available kernel to delete, ```jupyter kernelspec list```
3. To remove kernel from Jupyter Notebook, ```jupyter kernelspec uninstall flightpriceprediction```
4. For clean up, remove the entire folder, ```C:\Users\User\anaconda3\envs\FlightPricePrediction``` or ```conda remove --name FlightPricePrediction --all```

# 1_Data
Original dataset from, ```https://www.kaggle.com/datasets/shubhambathwal/flight-price-prediction```, Dataset.csv

# 2_Model
## EDA
More detail can refer ```./1_Data/report.html```
![Screenshot](./Screenshots/Report.png)

## Preprocess
- Drop column, 'Unnamed: 0' and 'flight' since both are no any meaningful.
- One hot encoding on another column, so all data will be 1 and 0 (True and False).
- For classifier, price need convert all contiounous data into 2 group (0 as budget and 1 as non budget) based on the median price.
- X: Entire One Hot Encoded and Cleaned Dataset exclude price column
- y: price column
-Data Spltting:
| :---: | :---: |
| Train | 80% |
| Test | 20% |

## Train
Model used for experimental purpose are RandomForestRegressor, LightGBMRegressor, RandomForestClassifier and LightGBMClassifier.

## Performance

| Model | Score (Before Grid Serach) | Score (After Grid Search) |
| :---: | :---: | :---: |
| RandomForestRegressor | 98.53% | 98.63% |
| LightGBMRegressor | 97.10% | 98.71% |
| RandomForestClassifier | 96.96% | 97.21% |
| LightGBMClassifier | 94.85% | 95.67% |

Importance Factor from each model:
| :---: | :---: |
| ![Screenshot](./Screenshots/RFC.png) | ![Screenshot](./Screenshots/RFR.png) |
| ![Screenshot](./Screenshots/LGBMC.png) | ![Screenshot](./Screenshots/LGBMR.png) |
