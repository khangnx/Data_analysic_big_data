
<img width="2243" height="1050" alt="JSON-preview" src="https://github.com/user-attachments/assets/429beb7c-ed4b-4de1-b4a1-5833b96e6688" />
# ✅ Giải thích sơ đồ:

```
Hadoop (HDFS): Lưu trữ dữ liệu CSV phân tán.
pandas: Đọc dữ liệu từ HDFS (sau khi tải về) và thực hiện phân tích thống kê.
spySpank: Kiểm tra chất lượng dữ liệu, phát hiện bất thường.
Flask: Cung cấp API để hiển thị kết quả phân tích cho người dùng.
```
# Luồng dữ liệu:

```
CSV được lưu trên HDFS.
pandas đọc và phân tích dữ liệu.
spySpank bổ sung kiểm tra chất lượng.
Flask trả kết quả qua API.
```
# File docker tạo demo hadoop

```
version: '2'
services:
  namenode:
    image: bde2020/hadoop-namenode:2.0.0-hadoop3.2.1-java8
    container_name: namenode
    ports:
      - "9870:9870"
      - "9000:9000"
    environment:
      - CLUSTER_NAME=test
      - CORE_CONF_fs_defaultFS=hdfs://namenode:9000
      - HDFS_CONF_dfs_replication=1
    volumes:
      - hadoop_namenode:/hadoop/dfs/name
    networks:
      - hadoop

  datanode:
    image: bde2020/hadoop-datanode:2.0.0-hadoop3.2.1-java8
    container_name: datanode
    ports:
      - "9864:9864"
    environment:
      - SERVICE_PRECONDITION=namenode:9870
      - CORE_CONF_fs_defaultFS=hdfs://namenode:9000
      - HDFS_CONF_dfs_replication=1
    volumes:
      - hadoop_datanode:/hadoop/dfs/data
    networks:
      - hadoop

volumes:
  hadoop_namenode:
  hadoop_datanode:

networks:
  hadoop:
    driver: bridge
```
# các lệnh cần chạy để tạo 1 dataNode trên hadoop

```
docker exec -it namenode bash #vào container hadoop name node
hdfs dfs -mkdir /user #tao folder chứa file data.csv
hdfs dfs -mkdir /user/hadoop  #tao folder chứa file data.csv
docker cp data.csv namenode:/tmp/data.csv #Copy file data.csv vào thu mực temp của docker
hdfs dfs -put /tmp/data.csv /user/hadoop/ #Upload file data.csv vào dataNode hadoop
Kiểm tra : hdfs dfs -ls /user/hadoop/
```
