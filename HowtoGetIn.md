# How to install a lab Core Analyse system

## Install Spark

See instructions at [Apache SPark](https://spark.apache.org/docs/latest/index.html)
Our test installation is [Spark Standalone Mode](https://spark.apache.org/docs/latest/spark-standalone.html)

#### 1. Install Java. We use java-11-openjdk.x86_64.
#### 2. Create an unprivileged user, in our case "sparkuser"
#### 3. Download Spark to unprivileged users home directory
#### 4. Configure Spark

Key packages we use for spark are: 

 - delta-lake (io.delta:delta-spark_...)
   This adds support for DeltaLake, a storage system based on Parquet files

 - standard HLL library (swoop:spark-alchemy_...)
   HLL libraries are generally different in the various databases that use them
   as the key function is to be as efficient as possible in approximating data
   within that database. The Aggregate Knowledge implementation of HLL is the
   closest thing to a wire format for HLL, which we use across the platform.

```
spark.eventLog.enabled             false
spark.eventLog.dir                 /tmp
spark.worker.cleanup.enabled       true
spark.jars.packages     io.delta:delta-spark_2.12:3.0.0,org.apache.hadoop:hadoop-aws:3.3.1,com.swoop:spark-alchemy_2.12:1.2.1,org.apache.spark:spark-sql_2.12:3.5.0,org.apache.spark:spark-streaming_2.12:3.5.0s,graphframes:graphframes:0.8.3-spark3.5-s_2.12

# S3 access parameters
spark.hadoop.fs.s3a.aws.credentials.provider                   com.amazonaws.auth.EnvironmentVariableCredentialsProvider
spark.hadoop.fs.s3a.endpoint                                   https://s3....
spark.hadoop.fs.s3a.endpoint.region                            us-east-1
spark.hadoop.fs.s3a.path.style.access                          true
spark.hadoop.fs.s3a.connection.ssl.enabled                     true
spark.hadoop.mapreduce.outputcommitter.factory.scheme.s3a      org.apache.hadoop.fs.s3a.commit.S3ACommitterFactory
spark.hadoop.fs.s3a.committer.staging.tmp.path                 /tmp/spark_staging
spark.hadoop.fs.s3a.buffer.dir                                 /tmp/spark_local_buf
spark.hadoop.fs.s3a.committer.staging.conflict-mode            fail

# Delta lake options
spark.delta.logStore.class                      org.apache.spark.sql.delta.storage.S3SingleDriverLogStore
spark.sql.extensions                            io.delta.sql.DeltaSparkSessionExtension
spark.sql.catalog.spark_catalog                 org.apache.spark.sql.delta.catalog.DeltaCatalog
```

## Install Jupyter Lab

It is probably wise to create a virtual python environment under the sparkuser user. We didn't.

```
pip install jupyterlab
```


## Install python libraries

boto3, paho...




# How to reach the spark / jupyter lab machine 

## Remote setup

For machine set up in on a Rocky VM. 

** Add ssh key to rocky user on <machine name/address> and connect **

`$ ssh rocky@<machine name/address>`

or

`$ ssh rocky@<machine name/address> -i ../path/to/private/key`

** Start spark/Jupyter **

The file .bashrc contains keys to S3 and other supporting systems, see below

```
export PATH=/sbin:/bin:/usr/sbin:/usr/bin:/usr/local/bin:/usr/local/scala/bin:/home/sparkuser/spark/bin:/home/sparkuser/spark/sbin
export SPARK_HOME=/home/sparkuser/spark
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk
export PYSPARK_DRIVER_PYTHON=jupyter
export PYSPARK_DRIVER_PYTHON_OPTS='lab'
export AWS_ACCESS_KEY_ID=<AWS key>
export AWS_SECRET_ACCESS_KEY=<AWS secret>
export AWS_ENDPOINT_URL=<S3 URL>
export AWS_REGION=us-east-1
```




```
$ su bash
# su sparkuser
$ . .bashrc
$ pyspark  --packages io.delta:delta-spark_2.12:3.0.0,org.apache.hadoop:hadoop-aws:3.3.1,com.swoop:spark-alchemy_2.12:1.2.1,org.apache.spark:spark-sql_2.12:3.5.0
```




**Find the auth token for Jupyter lab at the end of startup message**

```
Or copy and paste one of these URLs:
    http://localhost:8888/lab?token=008fa400b5cb95f096a3...
    http://127.0.0.1:8888/lab?token=008fa400b5cb95f096a3...
```

## Local setup

Add firefox to client machine
Add foxyproxy to firefox (saves the trouble of allowing "localhost capture")
Configure proxy: SOCKS5 on 127.0.0.1 port 1080 

**Use ssh SOCKS-proxy:**

`ssh -D 1080 rocky@192.121.209.113 -i ../path/to/private/key`

This session will sometimes be noisy with error messages, so leave it in a tab and use a diferent session to run commands or use -N


## Connect to jupyter lab

** Copy the Jupyter lab URL with token into Firefox: **

* See above: http://127.0.0.1:8888/lab?token=008fa400b5cb95f096a3... *

