# DAY 2 - 16/01/2024
### Việc làm hôm nay:
**1. Tìm hiểu các mô hình predict Multivariate Timeseries**
Tập trung tìm hiêu các mô hình mà có thể predict Multivariate Timeseries do Prophet hay ẢRIMA sử dụng cho Univariate Timeseries

***Bài toán mình đang sử dụng dự đoán xe:***
- **Input** có 1 bảng có cột ngày, tên xe, trọng tải và giá xe
Preprocessing fillna bằng KNNImputer (Đã kiểm tra hiệu quả nhất so với ffill, bfill và ETS)

- Với mô hình theo **Predict Univariate Timeseries**,  minh đã dùng Prophet, ARIMA và ETS Model để dự đoán từng xe một và chỉ sử dụng feature ngày

-> Kết quả prophet đạt kết quả tốt nhất tuy nhiên vẫn cần tìm thêm các mô hình khác xem hiệu quả tốt hơn không

- Với mô hình theo **Predict Multivariate Timeseries**, mình có thể đi theo 2 hướng: 
  - Một là thêm feature trọng tải.
  - Hai là dự đoán toàn bộ xe cùng 1 lúc.
  
-> Mình đi theo hướng 2. Input sẽ có cột ngày, giá xe, các xe và mình sẽ predict toàn bộ xe cùng lúc

-> Hiện tại mình đang tìm hiểu LightGBM (team cũng tìm hiểu song song LightGBM)

Mình đang follow theo 2 source: 
- https://forecastegy.com/posts/multivariate-time-series-forecasting-in-python/
- https://github.com/ugursaricam/store-item-demand-forecasting/blob/master/deman_forecasting.py
- https://www.kaggle.com/code/yugagrawal95/multivariate-timeseries-analysis-by-lgbm

***Source 1***, predict data dùng ML forecast
```
models = [LGBMRegressor(random_state=0, n_estimators=100, force_col_wise=True)]

model = MLForecast(models=models,
                   freq='D',
                   lags=[1,7,14],
                   lag_transforms={
                       1: [(rolling_mean, 7), (rolling_max, 7), (rolling_min, 7)],
                   },
                   date_features=['dayofweek', 'month'],
                   num_threads=6)


model.fit(train_lightgbm_uni, id_col='Hãng xe + hiệu xe', time_col='policy_issued_date', target_col='gia_xe', static_features=[])

p = model.predict(365)
```
-> Predict data ra kết quả khá tốt tuy nhiên chưa hiểu rõ **MLForecast** nên làm thêm theo hướng 2

***Source 2 + 3***, predict **LightGBM** qua library **lightgbm**. Tuy nhiên vẫn có một số vấn đề chưa hiểu
- Feature Engineering theo bài kaggle phần def các function lag_features, roll_mean_features và ewm_features đang chưa hiểu việc thêm các số trong hàm dựa theo đâu?
- set param trong LightGBM parameters đang dựa vào đâu?

-> Đang hiểu theo hướng là cần thử param = các số khác nhau. 
Tuỳ trường hợp có thể có các cách ước lượng trước khác nhau, VD như lag_features sẽ giống việc tìm p qua pacf. 
Tuy nhiên, thực tế cần thử các số khác nhau quanh số ước lượng để tìm kiếm kểt quả tốt nhất