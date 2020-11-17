# Apache Spark
This lab will introduce the basics of Spark and guide you through installing and running spark-shell in local and Standalone mode in Scala and Python.

* Download and test Scala:
  - `$ wget ...`
  - `$ tar ... `
  - `$ scalac -version`

[Scala MACOS](https://medium.com/@djamaldg/how-to-install-scala-on-macos-5771d55339cb)

* Download and test Spark:
  - `$ wget ...`
  - `$ tar ... `
  - Launch Spark shell `$ spark-shell `
  - Close Spark shekk `$ :q `


* Run spark examples ([local mode](http://spark.apache.org/docs/latest/)):
  - Scala:
  - Python:
  
## Run Wordcount in local Standalone mode from Spark Shell (Scala)
 * Run Spark master: `$ sbin/start-master.sh`
 * Check Spark master UI on browser at `localhost:8080`
 * Run Spark slave: `$ sbin/start-slave.sh <HOST:PORT.
 * Locate a textfile in your Spark home directory (e.g. README.md)
 * Launch interactive spark shell, using the master in local mode, with 4 threads for wordcount: `$ spark-shell --master "local[4]" `
 * Use Scala code for wordcount: <!--https://www.tutorialkart.com/apache-spark/scala-spark-shell-example/-->

 ```
 [scala> var map = sc.textFile("README.md").flatMap(line => line.split(" ")).map(word => (word,1));
 [scala> var counts = map.reduceByKey(_+_);
 [scala> counts.saveAsTextFile("output/");
 [scala> :q
```
 * Verify output: `$ cat output/part-0000 `
 * Run Wordcount in same mode but in Python as illustrated [here](https://www.tutorialkart.com/apache-spark/python-spark-shell-pyspark-example/)

## Note: Local vs Standalone Spark cluster 
We have said you can run Spark locally or on a distributed file system (Hadoop). Even when you are running spark locally (without Hadoop cluster running), you can either run it without a cluster (like when we run scala and python examples) or on standalone cluster mode, using spark cluster and no distributed file system. In this case (which is necessary for running examples such as wordcount) you need to launch the spark master and slave locally.

<!--MAC OS X
https://www.tutorialkart.com/apache-spark/how-to-install-spark-on-mac-os/-->


