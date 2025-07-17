# Linux Commands

## Log Generator and Data Pipeline Project - NTI Graduation Project

This document summarizes all the Linux terminal commands used throughout the NTI graduation project, along with explanations of their purpose and terminal usage structure.

---

## Initial Setup - Log Generator

* The log generator used in this project:

  > [log-generator](NTI-Graduation-Project/tree/main/logGenerator)

* The log generator directory was placed directly on the Desktop for easier access:

```bash
cd ~/Desktop/logGenerator/
```

* I accessed the log generator folder through its dedicated terminal and started generating log data using the following command:

```bash
python log_generator.py \
--logFile logs/sample.log \
--sourceDataFile defaultDataFile.txt \
--iterations 100000 > log_output.txt 2>&1
```

---

## Real-time Log Viewing

* In a separate terminal window, I monitored the logs live using:

```bash
tail -f logs/sample.log
```

---

## HDFS Setup

* In a third terminal, I started HDFS and YARN (commands like `start-dfs.sh` and `start-yarn.sh` were used).

* I created a dedicated directory on HDFS named "graduation" to store the incoming logs from Flume:

```bash
hdfs dfs -mkdir -p /user/bigdata/graduation
```

---

## Flume Setup

* I prepared the Flume configuration file called `flumeHdfs.conf`, located on the Desktop at the following path:

```plaintext
/home/bigdata/Desktop/flumeHdfs.conf
```

* In a new terminal session, I started Flume using the configuration file to transfer the logs from the log file to HDFS:

```bash
flume-ng agent \
--conf conf \
--conf-file /home/bigdata/Desktop/flumeHdfs.conf \
--name agent \
-Dflume.root.logger=INFO,console
```

---

## Jupyter Notebook & PySpark Setup

* In a separate terminal, I launched Jupyter Notebook to interact with PySpark through a web GUI:

```bash
jupyter notebook
```

* Inside the notebook, I initialized PySpark using the following Python commands:
    go to this file `/logreadergrad.ipynb`

```python
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("Graduation Project").getOrCreate()
```
