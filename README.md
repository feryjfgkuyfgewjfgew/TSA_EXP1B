# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
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


data = pd.read_csv('tsa.csv')
data['Date'] = pd.to_datetime(data['Date'])
data.set_index('Date', inplace=True)


data['close_diff'] = data['Close'] - data['Close'].shift(1)


result = seasonal_decompose(data['Close'], model='additive', period=30)

data['close_sea_diff'] = result.resid
data['close_log'] = np.log(data['Close'])
data['close_log_diff'] = data['close_log'] - data['close_log'].shift(1)


result_log = seasonal_decompose(data['close_log_diff'].dropna(), model='additive', period=30)
data['close_log_seasonal_diff'] = result_log.resid


plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data['Close'], label='Original')
plt.legend(loc='best')
plt.title('Original Close Price')
plt.xlabel('Date')
plt.ylabel('Close Price')

plt.subplot(6, 1, 2)
plt.plot(data['close_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Date')
plt.ylabel('Diff Close')

plt.subplot(6, 1, 3)
plt.plot(data['close_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Date')
plt.ylabel('Residuals')

plt.subplot(6, 1, 4)
plt.plot(data['close_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Date')
plt.ylabel('Log(Close)')

plt.subplot(6, 1, 5)
plt.plot(data['close_log_diff'], label='Log + Differencing')
plt.legend(loc='best')
plt.title('Log Transformation + Differencing')
plt.xlabel('Date')
plt.ylabel('Diff Log(Close)')

plt.subplot(6, 1, 6)
plt.plot(data['close_log_seasonal_diff'], label='Log + Differencing + Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Log + Regular Differencing + Seasonal Differencing')
plt.xlabel('Date')
plt.ylabel('Residuals')

plt.tight_layout()
plt.show()



plt.figure(figsize=(12, 8))
plt.plot(data['Close'], label='Close')
plt.plot(data['close_diff'], label='close_diff')
plt.plot(data['close_sea_diff'], label='close_sea_diff')
plt.plot(data['close_log'], label='close_log')
plt.plot(data['close_log_diff'], label='close_log_diff')
plt.plot(data['close_log_seasonal_diff'], label='close_log_seasonal_diff')
plt.legend(loc='best')
plt.show()

```

### OUTPUT:
ORIGINAL CLOSE PRICE:
<img width="1426" height="231" alt="Screenshot 2025-08-19 132848" src="https://github.com/user-attachments/assets/4f33514a-9d33-4086-aa24-313f0585f219" />



REGULAR DIFFERENCING:
<img width="1423" height="238" alt="Screenshot 2025-08-19 132910" src="https://github.com/user-attachments/assets/b515ca82-eee7-4bcd-9efe-0478dae186f9" />




SEASONAL ADJUSTMENT:
<img width="1422" height="223" alt="Screenshot 2025-08-19 132923" src="https://github.com/user-attachments/assets/26e08b82-65ea-47a2-94f1-6a418733f1e4" />



LOG TRANSFORMATION:
<img width="1412" height="224" alt="Screenshot 2025-08-19 132938" src="https://github.com/user-attachments/assets/6561e681-90db-4372-a495-988c00a65c4f" />

<img width="1420" height="217" alt="Screenshot 2025-08-19 133330" src="https://github.com/user-attachments/assets/0f4d5a9c-fc3d-4963-808d-f779b81580e4" />
<img width="1421" height="225" alt="Screenshot 2025-08-19 133346" src="https://github.com/user-attachments/assets/b0257c45-cf4d-48de-9115-1f17b4abd460" />
<img width="1027" height="648" alt="Screenshot 2025-08-19 133453" src="https://github.com/user-attachments/assets/274f8f3b-c53c-4191-ab1b-cef864355fa2" />







### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
