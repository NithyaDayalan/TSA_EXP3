# Ex.No : 03   COMPUTE THE AUTO FUNCTION(ACF)
## DATE : 18/03/2025 

## AIM :
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.

## ALGORITHM :
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
   
## PROGRAM :
```
Dveloped By : NITHYA D
Reg.no : 212223240110
```
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
file_path = "Gold Price Prediction.csv"
data = pd.read_csv(file_path)
data['Date'] = pd.to_datetime(data['Date'], errors='coerce')
data.dropna(subset=['Date'], inplace=True)
data.set_index('Date', inplace=True)
if 'Price Today' not in data.columns:
    print("Error: 'Price Today' column not found!")
else:
    data['Price Today'] = pd.to_numeric(data['Price Today'], errors='coerce')
    data.dropna(subset=['Price Today'], inplace=True)
    print("Missing values in 'Price Today':", data['Price Today'].isna().sum())
    print("Unique values in 'Price Today':", data['Price Today'].nunique())
    if data['Price Today'].nunique() > 1:
        prices = data['Price Today'].values
```
#### Mean and Variance : 
```
        mean_price = np.mean(prices)
        variance_price = np.var(prices)
        print(f"Mean: {mean_price}, Variance: {variance_price}")
```

#### Normalized data :   
```
        normalized_prices = prices - mean_price
```

#### Compute autocorrelation function (ACF)
```
        max_lag = 35
        acf_values = np.zeros(max_lag + 1)
        n = len(prices)
        for lag in range(max_lag + 1):
            autocovariance = np.sum(normalized_prices[:n-lag] * normalized_prices[lag:]) / n
            acf_values[lag] = autocovariance / variance_price
```

#### Display the graph
```
        plt.figure(figsize=(10, 6))
        plt.stem(range(max_lag + 1), acf_values, linefmt='b-', markerfmt='bo', basefmt='k-')
        plt.title('Autocorrelation Function (ACF) of Gold Prices')
        plt.xlabel('Lags')
        plt.ylabel('ACF')
        plt.grid(True)
        plt.show()
    else:
        print("Error: 'Price Today' contains only one unique value. ACF cannot be computed.")
```

## OUTPUT :
![image](https://github.com/user-attachments/assets/8974cdad-2782-4e4e-971a-8d19027b0786)
![image](https://github.com/user-attachments/assets/53e24567-774a-43b3-babd-438103270cbc)


## RESULT :
Thus we have successfully implemented the auto correlation function in python.
