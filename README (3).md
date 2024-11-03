
# Real-Time Data Processing Pipeline

This project is a data processing pipeline designed for real-time data ingestion, processing, and storage, leveraging Apache Kafka, Apache Flume, Apache Hadoop, and Spark, with visualization provided through Grafana and InfluxDB.

## Overview

This pipeline captures web server logs, processes them in real time, and stores them in both Hadoop (for long-term storage) and InfluxDB (for visualization in Grafana). The pipeline architecture ensures scalability, durability, and low latency.

![Pipeline Architecture](path-to-image) <!-- Replace `path-to-image` with the actual image path in the repository. -->

### Components

1. **Web Server (Log Source)**: Generates logs to be processed in real time.
2. **Apache Flume**: Collects logs from the web server and forwards them to Kafka.
3. **Apache Kafka**: Acts as a distributed messaging system to manage log streaming.
4. **Apache Hadoop**: Stores logs in HDFS for batch processing and analysis.
5. **Apache Spark** (Optional): Used for real-time processing if required.
6. **InfluxDB**: Time-series database for storing metrics.
7. **Grafana**: Visualization tool to monitor the pipeline metrics in real-time.

## Pipeline Flow

1. **Data Ingestion**: Web server logs are collected by Apache Flume and sent to Kafka.
2. **Data Streaming**: Kafka streams the logs to multiple sinks for parallel processing.
3. **Data Storage**:
   - Logs are sent to HDFS for long-term storage.
   - Metrics are stored in InfluxDB for visualization.
4. **Visualization**: Grafana pulls data from InfluxDB for real-time monitoring.

## Configuration Files

### 1. Kafka Configuration (in Spark)
Define Kafka configuration in your Spark application for data ingestion and streaming.

```python
# Kafka Configuration Example
kafka_bootstrap_servers = "localhost:9092"
kafka_topic = "pop"
```

### 2. Flume Configuration

**Agent 1** (Web Server Logs to Kafka):

```properties
# Flume Agent Configuration for Kafka
a1.sources.r1.type = spooldir
a1.sources.r1.spoolDir = /path/to/spooldir
a1.sinks.k1.type = org.apache.flume.sink.kafka.KafkaSink
a1.sinks.k1.kafka.topic = pop
```

**Agent 2** (Kafka to HDFS):

```properties
# Flume Agent Configuration for HDFS
a2.sources.r2.type = org.apache.flume.source.kafka.KafkaSource
a2.sinks.k2.type = hdfs
a2.sinks.k2.hdfs.path = /case_pop
```

### 3. Spark Application

Process data from Kafka in Spark with a schema applied to parse JSON data.

```python
# Initialize Spark session
spark = SparkSession.builder.appName("Kafka-PySpark-Integration").getOrCreate()
# Additional Spark code here
```

### 4. InfluxDB and Grafana Setup

InfluxDB is used for storing the real-time metrics data, which is then visualized using Grafana.

## How to Run the Project

1. Set up Kafka and Flume agents as per the configuration files provided.
2. Configure Spark to connect to Kafka for data streaming.
3. Deploy Grafana and InfluxDB to monitor the pipeline metrics.

## Prerequisites

- Apache Kafka
- Apache Flume
- Apache Hadoop
- Apache Spark (Optional)
- InfluxDB and Grafana for visualization

## Usage

- **Monitor Real-Time Data**: Use Grafana with InfluxDB as the data source to visualize and monitor real-time metrics.
- **Batch Processing**: Access stored logs in HDFS for batch processing and analysis.

## Future Improvements

- Integrate more real-time processing capabilities using Apache Spark or Apache Storm.
- Add automated alerting in Grafana for threshold-based monitoring.

## License

This project is licensed under the MIT License.
