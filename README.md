# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 24-02-2026

### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:

#### Name : Prakash C
#### Reg.No : 212223240122

import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

data=pd.read_csv('NSE-TATAGLOBAL11.csv',parse_dates=['Date'],index_col='Date')
resampled_data = data['Turnover (Lacs)'].resample('Y').sum().to_frame()
resampled_data.head()
resampled_data.reset_index(inplace=True)
resampled_data.rename(columns={'Date':'Year'}, inplace=True)
Years = resampled_data['Year'].tolist()
data = resampled_data['Turnover (Lacs)'].tolist()

N = len(data)

lags = range(35)

#Pre-allocate autocorrelation table
autocorr_values = []

#Mean
mean_data = np.mean(data)

#Variance
variance_data = np.var(data)

#Normalized data
normalized_data = (data - mean_data) / np.sqrt(variance_data)

#Go through lag components one-by-one
for lag in lags:
    if lag == 0:
        autocorr_values.append(1)
    else:
        auto_cov = np.sum((data[:-lag] - mean_data) * (data[lag:] - mean_data)) / N 
        autocorr_values.append(auto_cov / variance_data)  # Normalize by variance

#display the graph
plt.figure(figsize=(10, 6))
plt.stem(lags, autocorr_values)
plt.title('Autocorrelation of Data')
plt.xlabel('Lag')
plt.ylabel('Autocorrelation')
plt.grid(True)
plt.show()

### OUTPUT:

<img width="976" height="546" alt="image" src="https://github.com/user-attachments/assets/7d5a91fb-6a62-4a31-98e8-59b072e46d69" />


### RESULT:
        Thus we have successfully implemented the auto correlation function in python.
