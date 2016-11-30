# pykafka_cassandra.py
实现Kafka Consumer往Cassandra存储数据过程

# 使用库
cassandra-driver    https://github.com/datastax/python-driver
pykafka   https://github.com/Parsely/pykafka

# 配置环境
pip install -r requirements.txt

# 运行
用cqlsh创建keyspace和table：
CREATE KEYSPACE "stock" WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 1} AND durable_writes = 'true';
USE stock;
CREATE TABLE stock_analyzer (stock_symbol text, last_trade_date_time timestamp, last_trade_price float, PRIMARY KEY (stock_symbol,last_trade_date_time));

使用格式：
python pykafka-cassandra.py kafka_broker kafka_topic cassandra_ip keyspace table

假设Kafka和Cassandra运行ip都是192.168.99.101：
python pykafka-cassandra.py 192.168.99.101:9092 stock-analyzer 192.168.99.101 stock stock_analyzer
