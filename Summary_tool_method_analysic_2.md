# Hướng dẫn tổng hợp: Kafka, Spark Streaming và ETL từ MySQL lên Redshift
# 1. Apache Kafka là gì?
Kafka là một hệ thống message broker phân tán, dùng để truyền dữ liệu theo thời gian thực
giữa các hệ thống. Dữ liệu được tổ chức theo topic và partition, hỗ trợ khả năng mở rộng và
lưu trữ lâu dài.
# 2. Spark Streaming là gì?
Spark Streaming (hoặc Spark Structured Streaming) là module của Apache Spark dùng để xử
lý dữ liệu luồng (streaming) theo micro-batch hoặc liên tục. Nó có thể đọc dữ liệu từ Kafka,
xử lý bằng DataFrame và ghi ra các sink như S3, console, hoặc Redshift.
# 3. Kafka + Spark Streaming: Kiến trúc tích hợp
• Kafka đóng vai trò nguồn dữ liệu (stream).
• Spark Structured Streaming đọc dữ liệu từ Kafka bằng connector spark-sql-kafka0.10.
• Dữ liệu được xử lý bằng Spark và ghi ra sink như S3, Redshift, hoặc Kafka khác.
# 4. Ví dụ xử lý Kafka bằng PySpark
```
1 from pyspark.sql import SparkSession
2 from pyspark.sql.functions import expr
3
4 spark = SparkSession.builder.appName("KafkaSparkStreaming").getOrCreate()
5
6 # Đọc từ Kafka
7 df = spark.readStream \
8 .format("kafka") \
9 .option("kafka.bootstrap.servers", "localhost:9092") \
10 .option("subscribe", "my-topic") \
11 .load()
12
13 # Chuyển đổi dữ liệu
14 parsed_df = df.selectExpr("CAST(key AS STRING)", "CAST(value
AS STRING)")
15
16 # Ghi ra console
17 query = parsed_df.writeStream \
18 .outputMode("append") \
19 .format("console") \
20 .start()
21
22 query.awaitTermination()
```

# 5. So sánh Kafka và Pika
```
Tiêu chí Kafka Pika (RabbitMQ)
Kiến trúc Pub/Sub, log-based Queue-based
Lưu trữ Có thể lưu lâu dài Xóa sau khi tiêu thụ
Mở rộng Rất tốt Tốt nhưng giới hạn
Dùng cho Big data, realtime Microservices, task queue
```
# 6. So sánh Hadoop vs AWS DMS cho đồng bộ dữ liệu
```
Tiêu chí Hadoop AWS DMS
Mục tiêu Xử lý dữ liệu lớn Di chuyển dữ liệu
Tốc độ triển khai Chậm, phức tạp Nhanh, dễ cấu hình
Xử lý dữ liệu Có Không
Thời gian thực Không phù hợp Có thể gần realtime
```
# 7. Pipeline ETL từ MySQL lên Redshift

```
Luồng dữ liệu:
1 MySQL → AWS DMS → S3 → (Glue/Spark xử lý) → Redshift
2
Các bước:
1. Trích xuất dữ liệu từ MySQL bằng DMS hoặc Python.
2. Lưu dữ liệu vào S3 dưới dạng CSV hoặc Parquet.
3. Dùng Glue hoặc Spark để xử lý dữ liệu.
4. Dùng lệnh COPY để tải dữ liệu vào Redshift.
8. Ví dụ ETL bằng Python
1 import pymysql, pandas as pd, boto3, psycopg2
2
3 # Trích xuất từ MySQL
4 conn = pymysql.connect(host='mysql-host', user='user',
password='pass', db='sales')
5 df = pd.read_sql('SELECT * FROM orders', conn)
6 df.to_csv('/tmp/orders.csv', index=False)
7
8 # Upload lên S3
9 s3 = boto3.client('s3')
10 s3.upload_file('/tmp/orders.csv', 'your-bucket',
'orders/orders.csv')
11
12 # COPY vào Redshift
13 conn = psycopg2.connect(...)
14 cur = conn.cursor()
15 cur.execute("""
16 COPY orders FROM 's3://your-bucket/orders/orders.csv'
17 IAM_ROLE 'arn:aws:iam::your-role'
18 CSV IGNOREHEADER 1;
19 """)
20 conn.commit()
```

# 9. Hướng dẫn cài đặt Airflow bằng Docker

```
1. Cài Docker & Docker Compose.
2. Tạo thư mục airflow-docker và file docker-compose.yaml.
3. Khởi tạo Airflow bằng docker compose up airflow-init.
4. Chạy Airflow bằng docker compose up.
5. Truy cập tại http://localhost:8080 với tài khoản airflow/airflow.
10. DAG Airflow mẫu cho ETL
1 from airflow import DAG
2 from airflow.operators.python import PythonOperator
3 from datetime import datetime
4
5 with DAG('mysql_to_redshift_etl',
start_date=datetime(2023,1,1), schedule_interval='@daily',
catchup=False) as dag:
6 extract = PythonOperator(...)
7 upload = PythonOperator(...)
8 load = PythonOperator(...)
9
10 extract >> upload >> load
```
Airflow.
