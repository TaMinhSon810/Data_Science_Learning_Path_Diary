# DAY 8 - 22/01/2024
### Việc làm hôm nay:
Việc ngày hôm nay là check việc xây features dựa trên dates và giá xe thông qua library **tsfresh** hoặc **ROCKET** rồi dùng **LightGBM** xem kết quả tốt hơn không và tốt hơn như nào.

**tsfresh** hiểu đơn giản là 1 library tạo ra rất nhiều features khác nhau dựa trên trường date và gia_xe
```
from tsfresh import extract_features
extracted_features = extract_features(timeseries, column_id = "name_car", column_sort="policy_date", default_fc_parameters=ComprehensiveFCParameters())
```

Mình dùng vòng lặp for để tạo features cho các loại xe. Kết quả là out of memory :)) \
MÌnh check error thì biết **tsfresh** nếu set `default_fc_parameters=ComprehensiveFCParameters()` thì sẽ tạo hơn 1000 features khác nhau. Chính vì vậy, solution set `default_fc_parameters=MinimalFCParameters()` sẽ chỉ tạo hơn 10 features nên tránh bị out of memory

Tips: Có thể set **default_fc_parameters** theo 1 dictionary. Link settings của feature extractions
tsfresh.readthedocs.io/en/latest/text/feature_extraction_settings.html


Kết quả overfitting :| xét cả từng xe hoặc toàn bộ các xe. Mình cũng xét cả trường hợp input có và không fillna bằng **KNNImputer**.

Một phần nữa, Team mình đang chạy song song các models để ra giá xe và đang nghiên cứu để xem cách nào phù hợp để trả ra giá xe oke nhất cho Ban nghiệp vụ kiểm tra lại.

Một giải pháp đang đề xuất: Team mình có khoảng 30 xe có nhiều data cả trong PTI và thị trường \
-> Dùng trung bình và trung vị predict ra kết quả **(1)**

Dùng các model đang chạy để kiểm tra các xe này xem predict kết quả **(2)** nào sát với kết quả **(1)** nhất\
-> Chọn model phù hợp

Recommend của a Đức có thể xem **evaluation metric** trước khi nghiệm thu thực tế.