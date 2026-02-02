# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 02.02.2026

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on retail sales data
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
data=pd.read_csv('/retail_sales_dataset.csv')

data['Date']=pd.to_datetime(data['Date'])
data.set_index('Date',inplace=True)

data_aggregated = data.groupby(data.index)['Total Amount'].mean().to_frame()

data_aggregated['Total_Amount_diff']=data_aggregated['Total Amount']-data_aggregated['Total Amount'].shift(1)

data_aggregated['Total_Amount_log'] = np.log(data_aggregated['Total Amount'].replace(0, 1e-9))
data_aggregated['Total_Amount_log_diff']=data_aggregated['Total_Amount_log']-data_aggregated['Total_Amount_log'].shift(1)

result = seasonal_decompose(data_aggregated['Total_Amount_log_diff'].dropna(), model='additive', period=12)
data_aggregated['Total_Amount_log_seasonal_diff']=result.resid

plt.figure(figsize=(20, 24))
plt.subplot(2, 1, 1) 
plt.plot(data_aggregated['Total Amount'], label='Original') 
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Date')
plt.ylabel('Total Amount')
plt.subplot(2, 1, 1)
plt.plot(data_aggregated['Total_Amount_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Date')
plt.ylabel('Total Amount')
plt.subplot(1, 1, 1) 
plt.plot(data_aggregated['Total_Amount_log_seasonal_diff'], label='Log Transformation, Regular and Seasonal Differencing') 
plt.legend(loc='best')
plt.title('Seasonally Adjusted Data (Log Transformed and Differenced)') 
plt.xlabel('Date')
plt.ylabel('SDiff(RDiff(Log(Total Amount)))')
plt.subplot(2, 1, 1) 
plt.plot(data_aggregated['Total_Amount_log'], label='Log Transformation') 
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Date')
plt.ylabel('Log(Total Amount)')
plt.subplot(1, 1, 1) 
plt.plot(data_aggregated['Total_Amount_log_diff'], label='Log Transformation and Regular Differencing') 
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Date')
plt.ylabel('RDiff(Log(Total Amount))')
plt.subplot(1,1,1) 
plt.plot(data_aggregated['Total_Amount_log_seasonal_diff'], label='Log Transformation and Regular Differencing and Seasonal Differencing')
plt.legend(loc='best')
plt.title('Seasonally Adjusted Data (Log Transformed and Differenced)') 
plt.xlabel('Date')
plt.ylabel('SDiff(RDiff(Log(Total Amount)))') 
plt.tight_layout()
plt.show() 
```
### OUTPUT:
<img width="1165" height="439" alt="image" src="https://github.com/user-attachments/assets/bcdd22c7-e0ff-49ef-8408-9d57fee91799" />

<img width="858" height="492" alt="image" src="https://github.com/user-attachments/assets/53df6a5b-d981-4797-8c0b-b00d190df11a" />

<img width="1040" height="621" alt="image" src="https://github.com/user-attachments/assets/6050b77f-d64b-428d-8cc5-592558515b3e" />

REGULAR DIFFERENCING:
<img width="820" height="426" alt="image" src="https://github.com/user-attachments/assets/01443963-8b57-4ea2-8103-602f4e493860" />


SEASONAL ADJUSTMENT:
<img width="969" height="657" alt="image" src="https://github.com/user-attachments/assets/5a77aa70-a53e-4710-88be-bb40385a22ba" />


LOG TRANSFORMATION:

<img width="1185" height="674" alt="image" src="https://github.com/user-attachments/assets/16cf2667-2369-46ab-90e7-eefa402e903e" />

<img width="938" height="652" alt="image" src="https://github.com/user-attachments/assets/9e3786f0-dea2-4ee6-9570-af0b76aea42e" />

<img width="1281" height="685" alt="image" src="https://github.com/user-attachments/assets/3f5be178-9506-49f9-aad5-7b954426033a" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on retail sales data.
