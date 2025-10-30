# Hướng dẫn xử lý dữ liệu với Spark và Pandas

## 1. Phân tích và chuẩn hóa dữ liệu với SparkContext và Hadoop trước khi đưa vào Pandas
- SparkContext là điểm bắt đầu của mọi ứng dụng Spark. Nó kết nối với cluster và tạo RDD từ các nguồn dữ liệu như HDFS, S3, hoặc local file system.
- Hadoop thường được dùng để lưu trữ dữ liệu lớn (HDFS) và có thể tích hợp với Spark để đọc dữ liệu phân tán.
- Quy trình xử lý dữ liệu:
  1. Thu thập dữ liệu từ nhiều nguồn (CSV, TXT, JSON, Parquet…).
  2. Phân tích sơ bộ: kiểm tra định dạng, số lượng cột, kiểu dữ liệu.
  3. Chuẩn hóa: chuyển đổi kiểu dữ liệu, xử lý thiếu dữ liệu, gộp/chuẩn hóa tên cột.
  4. Chuyển sang Pandas: dùng .toPandas() để chuyển sang Pandas DataFrame để lọc và phân tích sâu.

## 2. Phân biệt SparkContext và SparkSession

| Thành phần       | SparkContext                         | SparkSession                          |
|------------------|--------------------------------------|----------------------------------------|
| Mục đích         | Khởi tạo ứng dụng Spark              | Giao diện thống nhất cho Spark APIs   |
| API hỗ trợ       | RDD                                  | RDD, DataFrame, SQL, Streaming, MLlib |
| Cách dùng        | sc = SparkContext()                  | spark = SparkSession.builder.getOrCreate() |
| Ưu điểm          | Đơn giản, truyền thống               | Hiện đại, hỗ trợ nhiều tính năng hơn  |

## 3. Các API trong Spark
- RDD (Resilient Distributed Dataset): cấu trúc dữ liệu phân tán, bất biến, xử lý dữ liệu thô.
- DataFrame: bảng dữ liệu có schema, giống Pandas nhưng phân tán.
- SQL: cho phép truy vấn dữ liệu bằng cú pháp SQL.
- Streaming: xử lý dữ liệu thời gian thực.
- MLlib: thư viện học máy của Spark.

## 4. Thư viện MLlib
- Hỗ trợ các thuật toán như:
  - Hồi quy tuyến tính, logistic
  - Cây quyết định, random forest
  - Clustering (KMeans)
  - PCA, SVD
- Tích hợp tốt với DataFrame và RDD.
- Có thể huấn luyện mô hình trên dữ liệu lớn phân tán.

## 5. Chuẩn hóa dữ liệu và mối liên hệ với 1NF, 2NF…
- Chuẩn hóa dữ liệu (data normalization): loại bỏ trùng lặp, chuẩn hóa kiểu dữ liệu, xử lý thiếu dữ liệu.
- Chuẩn hóa cơ sở dữ liệu (1NF, 2NF, 3NF...): quy tắc thiết kế bảng để tránh dư thừa và đảm bảo tính toàn vẹn.
- Hai khái niệm này liên quan nhưng không giống nhau.

## 6. Phân tích dữ liệu từ customer.csv và customers.txt
- Dùng SparkContext.textFile() để đọc cả hai file.
- Dùng .map() để phân tích từng dòng, tách các trường.
- Dùng .filter() để lọc khách hàng có số tiền > 2000 USD.
- Sau đó chuyển sang Pandas để xử lý chi tiết hơn.

## 7. Xử lý khi số cột không đồng nhất
- Dùng Spark để xác định schema của từng file.
- Thêm cột thiếu bằng cách:
  - Gán giá trị mặc định (null, "unknown", 0…).
  - Dùng .withColumn() để thêm cột vào DataFrame.
- Sau khi đồng bộ schema, có thể gộp dữ liệu lại.

## 8. Tự động hóa việc thêm cột
- Viết hàm kiểm tra schema của từng file.
- So sánh và xác định cột thiếu.
- Tự động thêm cột bằng Spark:
  from pyspark.sql.functions import lit
  df = df.withColumn("new_column", lit(None))
