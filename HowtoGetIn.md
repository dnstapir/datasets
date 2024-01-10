# How to reach the spark / jupyter lab machine 

## Remote setup

**Add ssh key to rocky user on 192.121.209.113 and connect**

`$ ssh rocky@192.121.209.113`

or

`$ ssh rocky@192.121.209.113 -i ../path/to/private/key`

**Start spark/Jupyter**

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

This session will sometimes be noisy with error messages, so leave it in a tab and use a diferent session to run commands


## Connect to jupyter lab

**Copy the Jupyter lab URL with token into Firefox:**

*See above: http://127.0.0.1:8888/lab?token=008fa400b5cb95f096a3...*

