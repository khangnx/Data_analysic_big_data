

## Hướng dẫn tổng hợp: Kafka, Spark Streaming và ETL từ MySQL lên Redshift
# 1. Apache Kafka là gì?
Kafka là một hệ thống message broker phân tán, dùng để truyền dữ liệu theo thời gian thực giữa các hệ thống. Dữ liệu được tổ chức theo topic và partition, hỗ trợ khả năng mở rộng và lưu trữ lâu dài.
# 2. Spark Streaming là gì?
Spark Streaming (hoặc Spark Structured Streaming) là module của Apache Spark dùng để xử lý dữ liệu luồng (streaming) theo micro-batch hoặc liên tục. Nó có thể đọc dữ liệu từ Kafka, xử lý bằng DataFrame và ghi ra các sink như S3, console, hoặc Redshift.
# 3. Kafka + Spark Streaming: Kiến trúc tích hợp

Kafka đóng vai trò nguồn dữ liệu (stream).
Spark Structured Streaming đọc dữ liệu từ Kafka bằng connector spark-sql-kafka-0.10.
Dữ liệu được xử lý bằng Spark và ghi ra sink như S3, Redshift, hoặc Kafka khác.
# 4. Ví dụ xử lý Kafka bằng PySpark

```
from pyspark.sql import SparkSession
from pyspark.sql.functions import expr

spark = SparkSession.builder.appName("KafkaSparkStreaming").getOrCreate()

# Đọc từ Kafka
df = spark.readStream \
    .format("kafka") \
    .option("kafka.bootstrap.servers", "localhost:9092") \
    .option("subscribe", "my-topic") \
    .load()

# Chuyển đổi dữ liệu
parsed_df = df.selectExpr("CAST(key AS STRING)", "CAST(value AS STRING)")

# Ghi ra console
query = parsed_df.writeStream \
    .outputMode("append") \
    .format("console") \
    .start()

query.awaitTermination()
```

# 5. So sánh Kafka và Pika
```
Tiêu chí	Kafka	Pika (RabbitMQ)
Kiến trúc	Pub/Sub, log-based	Queue-based
Lưu trữ	Có thể lưu lâu dài	Xóa sau khi tiêu thụ
Mở rộng	Rất tốt	Tốt nhưng giới hạn
Dùng cho	Big data, realtime	Microservices, task queue
```

# 6. So sánh Hadoop vs AWS DMS cho đồng bộ dữ liệu
```
Tiêu chí	Hadoop	AWS DMS
Mục tiêu	Xử lý dữ liệu lớn	Di chuyển dữ liệu
Tốc độ triển khai	Chậm, phức tạp	Nhanh, dễ cấu hình
Xử lý dữ liệu	Có	Không
Thời gian thực	Không phù hợp	Có thể gần realtime
```

# 7. Pipeline ETL từ MySQL lên Redshift
Luồng dữ liệu:
MySQL → AWS DMS → S3 → (Glue/Spark xử lý) → Redshift


Các bước:

Trích xuất dữ liệu từ MySQL bằng DMS hoặc Python.
Lưu dữ liệu vào S3 dưới dạng CSV hoặc Parquet.
Dùng Glue hoặc Spark để xử lý dữ liệu.
Dùng lệnh COPY để tải dữ liệu vào Redshift.
# 8. Ví dụ ETL bằng Python
```
import pymysql, pandas as pd, boto3, psycopg2

# Trích xuất từ MySQL
conn = pymysql.connect(host='mysql-host', user='user', password='pass', db='sales')
df = pd.read_sql('SELECT * FROM orders', conn)
df.to_csv('/tmp/orders.csv', index=False)

# Upload lên S3
s3 = boto3.client('s3')
s3.upload_file('/tmp/orders.csv', 'your-bucket', 'orders/orders.csv')

# COPY vào Redshift
conn = psycopg2.connect(...)
cur = conn.cursor()
cur.execute("""
    COPY orders FROM 's3://your-bucket/orders/orders.csv'
    IAM_ROLE 'arn:aws:iam::your-role'
    CSV IGNOREHEADER 1;
""")
conn.commit()
```

# 9. Hướng dẫn cài đặt Airflow bằng Docker

Cài Docker & Docker Compose.
Tạo thư mục airflow-docker và file docker-compose.yaml.
Khởi tạo Airflow bằng docker compose up airflow-init.
Chạy Airflow bằng docker compose up.
Truy cập tại http://localhost:8080 với tài khoản airflow/airflow.
# 10. DAG Airflow mẫu cho ETL
```
from airflow import DAG
from airflow.operators.python import PythonOperator
from datetime import datetime

with DAG('mysql_to_redshift_etl', start_date=datetime(2023,1,1), schedule_interval='@daily', catchup=False) as dag:
    extract = PythonOperator(...)
    upload = PythonOperator(...)
    load = PythonOperator(...)

    extract >> upload >> load
```
