# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 28/04/26

### AIM:
To perform regular differncing,seasonal adjustment and log transformation on international airline passenger data

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.


### PROGRAM:
```

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose



data = pd.read_csv('/content/AirPassengers.csv', parse_dates=['Month'])
data.set_index('Month', inplace=True)


data['passengers_diff'] = data['#Passengers'].diff()
data['passengers_log'] = np.log(data['#Passengers'])
data['passengers_log_diff'] = data['passengers_log'].diff()

data['passengers_sea_diff'] = seasonal_decompose(
    data['#Passengers'], model='additive', period=12
).resid

data['passengers_log_seasonal_diff'] = seasonal_decompose(
    data['passengers_log_diff'].dropna(), model='additive', period=12
).resid


plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 2)
plt.plot(data['passengers_diff'], label='Regular Difference')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced No of passengers')
plt.legend()

plt.subplot(6, 1, 3)
plt.plot(data['passengers_sea_diff'], label='Seasonal Adjustment')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Seasonally adjusted No of passengers')
plt.legend()

plt.subplot(6, 1, 4)
plt.plot(data['passengers_log'], label='Log Transformation')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(No of passengers)')
plt.legend()

plt.tight_layout()
plt.show()
```

### OUTPUT:


REGULAR DIFFERENCING:

<img width="1472" height="253" alt="image" src="https://github.com/user-attachments/assets/961f1cd6-3cc4-432f-9fd8-e32667163f62" />




SEASONAL ADJUSTMENT:
<img width="1452" height="269" alt="image" src="https://github.com/user-attachments/assets/0f17db02-64d1-44a8-93da-0002a921bb80" />


LOG TRANSFORMATION:

<img width="1435" height="259" alt="image" src="https://github.com/user-attachments/assets/ab792918-b40e-40f2-9d7c-388dde83dcc7" />



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
