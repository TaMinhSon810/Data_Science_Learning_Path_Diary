# DAY 1 - 15/01/2024
### Việc làm hôm nay:
**1. Predict data timeseries thông qua mô hình ARIMA**
ARIMA - Autoregressive Intergrated Moving Average
https://phamdinhkhanh.github.io/2019/12/12/ARIMAmodel.html

**2. Determine order of arima model p, d, q thông qua ACF, PCAF và adfuller**
- p (AR Order) is the number of autoregressive terms 
- d (Order of Differencing) is the number of nonseasonal differences
- q (MA Order) is the number of lagged forecast errors in the prediction equation 
**Cách xác định**
*d*: 
Check stationary thông qua dùng adfuller
```from statsmodels.tsa.stattools import adfuller

# Example ADF test
result = adfuller(df['your_column'])
print('ADF Statistic:', result[0])
print('p-value:', result[1])
```
Result: Nếu có p-value < 0.05 -> có tính stationary. 
        Ngược lại không phủ nhận được giả thuyết timeseries không có tính stationary. 
-> Check stationary ta sẽ xác định có cần phải differencing không
-> Xác định ddược d

*p*: Xác định thông qua PACF
```
from statsmodels.graphics.tsaplots import plot_pacf

plot_pacf(time_series, lags=20)
```
-> Xác định p có spike dot gần 1 nhất -> strong correlation


*q*: Xác định thông qua ACF
```
from statsmodels.graphics.tsaplots import plot_acf

plot_acf(time_series, lags=20)
```
-> Xác định q có spike dot sát với significant area (vùng xanh nhạt) nhất

**Source**:
- https://analyticsindiamag.com/quick-way-to-find-p-d-and-q-values-for-arima/
- https://www.youtube.com/watch?v=_qv_7lEuiZg&t=1168s