## Tổng hợp công nghệ Big Data và Data Analysis kết hợp với Python

### 1. Hệ thống xử lý phân tán

- **Apache Spark (PySpark)**: Là framework xử lý dữ liệu lớn theo mô hình phân tán. PySpark là API Python của Spark, cho phép xử lý dữ liệu dạng RDD (Resilient Distributed Dataset) và DataFrame. Spark hỗ trợ cả xử lý batch (dữ liệu theo lô) và streaming (dữ liệu thời gian thực).
#  Cách Pyspank chuẩn hóa, kiểm tra data
        🧼 1. Chuẩn hóa dữ liệu (Normalization)
        Pyspank thực hiện chuẩn hóa thông qua các bước sau:
        a. Loại bỏ khoảng trắng và ký tự đặc biệt
        
        Tự động loại bỏ khoảng trắng dư thừa ở đầu/cuối chuỗi.
        Chuẩn hóa các ký tự đặc biệt, ví dụ: chuyển “” thành " hoặc ‘’ thành '.
        
        b. Đổi tên cột (Column Renaming)
        
        Chuyển tên cột về định dạng chuẩn: viết thường, thay khoảng trắng bằng dấu gạch dưới (_), loại bỏ ký tự không hợp lệ.
        Ví dụ: "Tên khách hàng" → "ten_khach_hang"
        
        c. Chuẩn hóa kiểu dữ liệu (Data Type Normalization)
        
        Tự động nhận diện và chuyển đổi kiểu dữ liệu phù hợp: ngày tháng, số, chuỗi.
        Ví dụ: "2025-10-29" → kiểu datetime, "1,000" → kiểu int.
        
        d. Xử lý giá trị thiếu (Missing Values)
        
        Phát hiện các giá trị thiếu như "NA", "null", "?", "" và chuyển thành np.nan.
        Có thể cấu hình để điền giá trị mặc định hoặc loại bỏ dòng chứa giá trị thiếu.
        
        
        🔍 2. Kiểm tra dữ liệu (Validation)
        Pyspank cung cấp các công cụ kiểm tra dữ liệu trước khi đưa vào pandas:
        a. Kiểm tra định dạng cột
        
        Xác minh xem các cột có đúng định dạng mong muốn không (ví dụ: cột ngày phải là kiểu datetime).
        Báo lỗi nếu có cột sai định dạng.
        
        b. Kiểm tra giá trị bất thường (Outliers)
        
        Phát hiện các giá trị nằm ngoài khoảng hợp lý (ví dụ: tuổi > 120).
        Có thể cấu hình ngưỡng kiểm tra.
        
        c. Kiểm tra trùng lặp (Duplicates)
        
        Phát hiện các dòng trùng lặp hoàn toàn hoặc theo một số cột nhất định.
        Có thể tự động loại bỏ hoặc cảnh báo.
        
        d. Kiểm tra tính nhất quán (Consistency)
        
        Kiểm tra xem các giá trị trong một cột có đồng nhất không (ví dụ: cột giới tính chỉ nên có Nam, Nữ).
        Phát hiện lỗi chính tả hoặc viết hoa/thường không đồng nhất.


- **Apache Flink (PyFlink)**: Tập trung vào xử lý dữ liệu streaming với độ trễ thấp. PyFlink là API Python cho phép viết các hàm xử lý tùy chỉnh. Flink phù hợp với các ứng dụng cần phản hồi nhanh như phân tích log, giao dịch tài chính.

- **Apache Hadoop**: Gồm HDFS (hệ thống lưu trữ phân tán) và MapReduce (mô hình xử lý dữ liệu). Python thường dùng để viết các script ETL hoặc tích hợp với các công cụ như Hive, Pig.

### 2. Thư viện xử lý dữ liệu lớn thuần Python

- **Dask**: Cho phép xử lý dữ liệu lớn bằng cách chia nhỏ và xử lý song song. Dask tương thích với Pandas và NumPy, nhưng có thể xử lý dữ liệu vượt quá bộ nhớ RAM.

- **Pandas**: Thư viện phổ biến nhất để thao tác dữ liệu dạng bảng. Hỗ trợ lọc, nhóm, thống kê, xử lý dữ liệu thiếu, merge/join,…

- **NumPy**: Cung cấp cấu trúc mảng đa chiều và các phép toán số học hiệu năng cao. Là nền tảng cho nhiều thư viện khoa học khác.

- **SciPy**: Mở rộng NumPy với các thuật toán toán học như tích phân, tối ưu hóa, thống kê, xử lý tín hiệu,…

### 3. Phân tích và trực quan hóa dữ liệu

- **Matplotlib**: Thư viện vẽ biểu đồ cơ bản như line, bar, scatter,… Có thể tùy chỉnh chi tiết từng thành phần của biểu đồ.

- **Seaborn**: Dựa trên Matplotlib, cung cấp các biểu đồ thống kê đẹp mắt như heatmap, boxplot, violin plot,…

- **Plotly**: Cho phép tạo biểu đồ tương tác, hỗ trợ hiển thị trên web, dashboard.

- **Statsmodels**: Dùng cho phân tích thống kê như hồi quy tuyến tính, kiểm định giả thuyết, phân tích chuỗi thời gian.

### 4. Machine Learning và Deep Learning

- **Scikit-learn**: Thư viện ML cổ điển, hỗ trợ các thuật toán như SVM, Random Forest, KNN, PCA,… Dễ sử dụng và tích hợp với Pandas.

- **TensorFlow / Keras**: Framework mạnh mẽ cho deep learning. Keras là API cấp cao của TensorFlow, giúp xây dựng mạng neural dễ dàng.

- **PyTorch**: Framework deep learning linh hoạt, phổ biến trong nghiên cứu và ứng dụng NLP, Computer Vision.

- **NLTK / SpaCy**: Dùng cho xử lý ngôn ngữ tự nhiên như phân tích cú pháp, tách từ, gán nhãn từ loại, nhận diện thực thể,…

### 5. Hệ thống quản lý và streaming dữ liệu

- **Apache Kafka**: Hệ thống truyền dữ liệu theo mô hình publish-subscribe. Dùng để thu thập và phân phối dữ liệu thời gian thực.

- **Apache Storm**: Xử lý dữ liệu streaming theo topology. Mỗi node xử lý một phần dữ liệu và truyền tiếp.

- **Google BigQuery**: Kho dữ liệu đám mây của Google, hỗ trợ truy vấn SQL tốc độ cao. Có thể tích hợp với Python qua thư viện `google-cloud-bigquery`.

### 6. Orchestration - Quản lý luồng ETL

- **Apache Airflow**: Quản lý pipeline dữ liệu bằng DAG (Directed Acyclic Graph). Cho phép lập lịch, retry, theo dõi trạng thái từng bước.

- **Luigi**: Tương tự Airflow, nhưng đơn giản hơn. Dùng để xây dựng pipeline ETL có phụ thuộc giữa các bước.

- **Prefect**: Thế hệ mới của Airflow, dễ tích hợp, hỗ trợ xử lý lỗi, retry, logging tốt hơn.

### 7. Cơ sở dữ liệu hỗ trợ Python

- **HBase / Cassandra**: Cơ sở dữ liệu NoSQL dạng cột, phù hợp với dữ liệu phi cấu trúc, có khả năng mở rộng cao.

- **Elasticsearch**: Dùng để tìm kiếm và phân tích dữ liệu dạng tài liệu (JSON). Phù hợp với log, dữ liệu văn bản.

- **Presto / Apache Drill**: Engine SQL phân tán, cho phép truy vấn dữ liệu từ nhiều nguồn như HDFS, S3, Cassandra,…

### 8. Tổng quan pipeline phân tích dữ liệu lớn

|Giai đoạn|Công nghệ tiêu biểu|
|---|---|
|Ingestion|Kafka, Python script, APIs, Airflow/Luigi|
|Storage|HDFS (Hadoop), BigQuery, HBase, Cassandra|
|Processing|PySpark, PyFlink, Dask, Scikit-learn, TensorFlow, PyTorch|
|Orchestration|Apache Airflow, Luigi, Prefect|
|Visualization|Matplotlib, Seaborn, Plotly|
|ML/AI|Scikit-learn, TensorFlow, Keras, PyTorch, NLTK|

### Ghi chú

- Python là ngôn ngữ trung tâm trong hệ sinh thái phân tích dữ liệu lớn.
- Có thể tích hợp Python với hầu hết các công nghệ hiện đại trong Big Data.
- Tùy theo quy mô và mục tiêu dự án, chọn công nghệ phù hợp để tối ưu hiệu quả.

