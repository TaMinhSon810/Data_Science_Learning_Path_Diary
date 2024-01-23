# DAY 8 - 22/01/2024
### Việc làm hôm nay:

Hôm nay chỉ check test code LightGBM và search giá niêm yết các xe...

LightGBM mình nhận ra là việc mình groupby theo hãng hiệu xe và ngày + tạo features qua tsfresh ra mean, median,... thì chính là giá xe\
-> Việc test data vs tập X_test có các features ~ gía xe không thể chứng minh được mô hình tốt hay k được\
-> cần sửa lại

Xem qua chút evaluation metrics thấy thực chất việc test các chỉ số R-squared, MSE, RMSE \
-> Regression Evaluation Metrics\
-> Cần xem thêm

