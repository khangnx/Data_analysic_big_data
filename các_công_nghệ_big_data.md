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

### **** Hadoop: Hadoop không chỉ đóng vai trò như một data warehouse phân tán, mà còn có thể đảm nhiệm nhiều chức năng khác trong hệ sinh thái xử lý dữ liệu lớn. Dưới đây là các vai trò và ứng dụng chính của Hadoop:

        ## 1. Hệ thống lưu trữ phân tán (Distributed Storage System)
        - HDFS (Hadoop Distributed File System) cho phép lưu trữ dữ liệu lớn trên nhiều máy chủ, đảm bảo tính chịu lỗi và khả năng mở rộng.
        - Dữ liệu được chia nhỏ và lưu trên nhiều node, giúp xử lý song song hiệu quả.
        
        ## 2. Hệ thống xử lý dữ liệu phân tán (Distributed Processing)
        - MapReduce là mô hình lập trình cho phép xử lý dữ liệu lớn theo cách song song và phân tán.
        - Thích hợp cho các tác vụ như lọc, tổng hợp, phân tích log, ETL.
        
        ## 3. Nền tảng cho các công cụ phân tích dữ liệu
        Hadoop là nền tảng cho nhiều công cụ phân tích dữ liệu lớn:
        
        | Công cụ | Mô tả |
        |--------|------|
        | Hive | Ngôn ngữ SQL-like để truy vấn dữ liệu trên HDFS |
        | Pig | Ngôn ngữ kịch bản xử lý dữ liệu bán cấu trúc |
        | Spark | Xử lý dữ liệu nhanh hơn MapReduce, hỗ trợ in-memory |
        | HBase | Cơ sở dữ liệu NoSQL phân tán, chạy trên HDFS |
        | Mahout | Thư viện học máy (machine learning) trên Hadoop |
        | Oozie | Công cụ quản lý workflow cho các job Hadoop |
        
        ## 4. Lưu trữ và xử lý dữ liệu phi cấu trúc
        - Hadoop có thể xử lý dữ liệu từ nhiều nguồn: log web, video, hình ảnh, âm thanh, dữ liệu cảm biến IoT…
        - Thích hợp cho các hệ thống phân tích hành vi người dùng, phân tích mạng xã hội, dữ liệu y tế…
        
        ## 5. Hỗ trợ hệ thống real-time và batch
        - Dù Hadoop truyền thống thiên về batch processing, nhưng khi kết hợp với Spark Streaming, Kafka, Flink… có thể xử lý dữ liệu thời gian thực.
        
        ## 6. Ứng dụng trong AI/ML
        - Dữ liệu lớn được lưu trữ và xử lý bằng Hadoop có thể dùng để huấn luyện mô hình AI/ML.
        - Kết hợp với Mahout hoặc Spark MLlib để triển khai các thuật toán học máy.
        
        ## 7. ETL và Data Lake
        - Hadoop thường được dùng làm data lake lưu trữ dữ liệu thô từ nhiều nguồn.
        - Sau đó dùng Hive, Spark hoặc Presto để xử lý và trích xuất dữ liệu phục vụ phân tích.
        
        ---
        
        # Tư vấn kiến trúc Hadoop cho dự án
        
        ## 1. Tổng quan kiến trúc Hadoop
        
        Hadoop gồm 4 thành phần lõi (HDFS, YARN, MapReduce, Common), chạy theo mô hình Master–Slave trên đa node:
        
        - **HDFS**: lưu dữ liệu phân mảnh thành block, lưu trên DataNode, quản lý metadata bởi NameNode với cơ chế replication để chịu lỗi.
        - **YARN**: ResourceManager (Master) phân phối tài nguyên, NodeManager (Slave) chịu trách nhiệm chạy task, cho phép chạy cả MapReduce và Spark.
        - **MapReduce**: xử lý batch theo mô hình song song với Mapper → Shuffle → Reducer.
        - **Hadoop Common**: thư viện dùng chung hỗ trợ các module trên.
        
        ## 2. Kiến trúc hệ thống đề xuất
        ```
        Clients/API
           ↓
        Ingress Layer (Kafka, NiFi, Flume)
           ↓
        HDFS Storage (raw & processed)
           ↓
        Processing Layer (YARN: MapReduce / Spark / Hive / Pig)
           ↓
        Data Lakezone (curated/analytics)
           ↓
        Serving Layer (HBase / Hive Thrift / Impala / Presto)
           ↓
        BI / ML / Analytics
        
        ```
        ## 3. Best Practices
        
        - Phân vùng dữ liệu theo thời gian.
        - Replication HDFS = 3.
        - Tách layer lưu trữ: raw, curated, analytics.
        - Dùng Spark cho xử lý nhanh, MapReduce cho batch truyền thống.
        - Giám sát cluster bằng Ganglia, Cloudera Manager.
        
        ## 4. Tích hợp với AWS
        
        ### A. Dùng EMR:
        - Quản lý cluster tự động.
        - Tích hợp S3, Auto Scaling, CloudWatch.
        
        ### B. Tự triển khai trên EC2:
        - Dùng EBS cho lưu trữ, snapshot để backup.
        - Lưu dữ liệu lâu dài lên S3 qua S3A hoặc distcp.
        
        ### Ví dụ triển khai trên AWS
        
        | Node Type   | Instance Type | Role                             |
        |-------------|----------------|----------------------------------|
        | Master      | m5.xlarge      | NameNode, ResourceManager        |
        | Core/Worker | r5.2xlarge     | DataNode, NodeManager, Spark     |
        | Utility     | t3.large       | Zookeeper, HiveServer, Oozie     |
        | AWS Storage | S3 + EBS       | Data persistence, backup         |
        
        ---
        
        ## 📌 Tổng kết
        
        - Hadoop phù hợp làm data lake, batch ETL, phân tích dữ liệu lớn.
        - Kiến trúc nên phân lớp rõ ràng để dễ bảo trì và mở rộng.
        - AWS EMR giúp triển khai nhanh, EC2 giúp kiểm soát sâu.
        - Áp dụng best practices để tối ưu chi phí và hiệu năng.
                ```
               
### Ghi chú

- Python là ngôn ngữ trung tâm trong hệ sinh thái phân tích dữ liệu lớn.
- Có thể tích hợp Python với hầu hết các công nghệ hiện đại trong Big Data.
- Tùy theo quy mô và mục tiêu dự án, chọn công nghệ phù hợp để tối ưu hiệu quả.

