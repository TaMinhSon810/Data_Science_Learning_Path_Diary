# DAY 4 - 18/01/2024
### Việc làm hôm nay:
Việc ngày hôm nay tiếp tục ngâm cứu predict data qua **MLForecast**.

Mình research thêm về **MLForecast** liệu bản thân hàm này tốt trong việc predict tức là **handle interdependencies** nên tốt hơn **Prophet** hay đơn thuần chỉ mang tính chất phụ trợ cho các ML models predict data timeseries.

Lý do là sáng nay sếp bảo mình thử thay model là **LinearRegression** + **MLForecast** thì kết quả cũng same same với các kết quả kia :D Nên mình research lại xem bản chất hàm chạy như nào.

Mình đọc chút source code và các docs liên quan đến **MLForecast** thì rất khó tìm cơ chế hoạt động của **MLForecast** do quá ít tài liệu hay blogs nên mình có hỏi Copilot và xem các nguồn Copilot dẫn. \
Kết quả khá hay, theo mình thấy **MLForecast** sẽ có 2 tác dụng chính:
- Giúp cho các ML models scikit-learn (**LightGBM**, **XGBoost**,...) có thể predict data trong các khoảng thời gian mong muốn (VD như 3 ngày, 5 ngày tiếp theo)
- Tự động làm **feature engineering** dựa trên việc set các param: tạo các feature liên quan đến **lagged values**, **rolling statistics** hay **dates attributes** để góp phần làm input cho model mình dùng.

Về **feature engineering**, **MLForecast** tạo ra rất nhiều features liên quan đến date. Sếp muốn mình check lại việc này thông qua việc dùng một technique khác trong **feature engineering** đó là việc xây features dựa trên dates thông qua library **tsfresh** hoặc **ROCKET** rồi dùng **LightGBM** xem kết quả tốt hơn. \
Xem theo link này để hiểu rõ hơn :D

https://github.com/blue-yonder/tsfresh/blob/main/notebooks/01%20Feature%20Extraction%20and%20Selection.ipynb

Nếu kết quả tốt như khi dùng **MLForecast** thì mình sẽ cơ bản hiểu rõ ràng việc **MLForecast** đang làm gì. Nhưng việc này thứ 2 mình mới check được do mai mình nghỉ phép ở nhà rồi xD

Một phần bên mình đang làm song song mình muốn note lại:\
 Chạy bài toán NER và dùng account **ChatGPT** 3.5 để làm. \
 Chi tiết công việc: Bên mình crawl data web về xe tải để có thông tin xe nhưng nội dung các trang web rất khác nhau. Do vậy làm thế nào để có thể extract các dữ liệu như hãng xe, hiệu xe, thông tin chi tiết xe thành các cột từ các trang web đó?\
 Bên mình đang bắt đầu chạy thử bằng cách dùng **openai** và **dotenv** để train cho **ChatGPT** để phân biệt. Sếp mình bảo đây là các task của mấy ông Prompt Engineering thì phải :| 

 Note thêm cái nữa là anh Đức recommend mình đọc tiếp về **Recommendation System**.