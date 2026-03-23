# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 02/02/2026
## Reg No:212224240053

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
data=pd.read_csv('/content/Tesla Dataset.csv')
data.head()

data['Date']=pd.to_datetime(data['Date'])
data.set_index('Date',inplace=True)
data['open_diff']=data['Open']-data['Open'].shift(1)
result = seasonal_decompose(data['Open'], model='additive', period=12)
data['open_sea_diff']=result.resid
data['open_log'] = np.log(data['Open'])
data['open_log_diff']=data['open_log']-data['open_log'].shift(1)

result = seasonal_decompose(data['open_log_diff'].dropna(), model='additive', period=12)
data['open_log_seasonal_diff']=result.resid

plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data['Open'], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('date')
plt.ylabel('Open')

plt.subplot(6, 1, 2)
plt.plot(data['open_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('date')
plt.ylabel('open')

plt.subplot(6, 1, 3)
plt.plot(data['open_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('date')
plt.ylabel('open')

plt.subplot(6, 1, 4)
plt.plot(data['open_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Date')
plt.ylabel('Log(No of open)')

plt.subplot(6, 1, 5)
plt.plot(data['open_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Date')
plt.ylabel('RDiff(Log(No of open))')

plt.figure(figsize=(16, 16))
plt.subplot(6, 1, 6)
plt.plot(data['open_log_seasonal_diff'], label='Log Transformation and regular Differencing and Seasonal Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing and Seasonal Differencing')
plt.xlabel('Date')
plt.ylabel('SDiff(RDiff(Log(No of open)))')

plt.tight_layout()
plt.show()

data.plot(kind='line')


### OUTPUT:

## ORIGINAL DATASET:

<img width="1646" height="383" alt="image" src="https://github.com/user-attachments/assets/a503edef-1d1c-495a-882b-67dc87d523df" />

## REGULAR DIFFERENCING:

<img width="1441" height="395" alt="image" src="https://github.com/user-attachments/assets/525c00f3-9863-43cf-918f-b5bad2552c5f" />

## SEASONAL ADJUSTMENT:

<img width="1455" height="408" alt="image" src="https://github.com/user-attachments/assets/3b98f49c-db05-4ef9-b0bc-b0751e020b3f" />

## LOG TRANSFORMATION:

<img width="1413" height="400" alt="image" src="https://github.com/user-attachments/assets/2ae0f8ab-e1b7-4de8-9363-34c0350ef1f0" />

## LOG TRANSFORMATION and REGULAR DIFFERENCING and SEASONAL DIFFERENCING:

<img width="1691" height="400" alt="image" src="https://github.com/user-attachments/assets/0e0b1296-eeea-42ef-b66f-024ea83c17be" />

## OVERALL VIEW:

<img width="866" height="726" alt="image" src="https://github.com/user-attachments/assets/8a79c717-7f1a-434a-92b3-2ca511b95fe5" />




### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
