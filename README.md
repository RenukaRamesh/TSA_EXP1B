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
<img width="1035" height="402" alt="image" src="https://github.com/user-attachments/assets/10a7b24b-f698-40f4-ae58-87b62842daa8" />

<img width="1054" height="387" alt="image" src="https://github.com/user-attachments/assets/127bdae2-5f51-4d16-9aae-5071c9d70add" />

<img width="753" height="429" alt="image" src="https://github.com/user-attachments/assets/fabaaf94-7786-4c8a-b383-4c681a3b45f3" />


REGULAR DIFFERENCING:

<img width="736" height="432" alt="image" src="https://github.com/user-attachments/assets/a6cd62a0-3eec-41c1-9d32-6a573f02ee60" />


SEASONAL ADJUSTMENT:

<img width="1223" height="722" alt="image" src="https://github.com/user-attachments/assets/ede48b09-4610-491b-970d-0e5d72c60a46" />


LOG TRANSFORMATION:

<img width="868" height="511" alt="image" src="https://github.com/user-attachments/assets/02f53581-fdd3-4b89-baec-1013aca9eafa" />

<img width="917" height="647" alt="image" src="https://github.com/user-attachments/assets/4c466bb7-3a19-4ccb-953c-acf932020455" />

<img width="1182" height="670" alt="image" src="https://github.com/user-attachments/assets/28c57c9a-7621-4d68-9ae9-b90489494423" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on retail sales data.
