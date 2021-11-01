# Apache Spark
This lab will introduce the basics of Spark and guide you through installing and running spark-shell in local and Standalone mode in Scala and Python.

## Download and test Scala:

  - Get latest version on Ubuntu:  `$ sudo apt-get install scala`
  - Alternatively you can get the sources: `$ wget https://downloads.lightbend.com/scala/2.12.3/scala-2.12.3.tar.gz`
  - Unzip sources: `$ tar -xvzf scala-2.12.3.tar.gz `
  - Move: `$ mv scala-2.12.3 /usr/local/scala`
  - Set env. variable: `$ export SCALA_HOME="/usr/local/scala" `
  - Add to PATH: `$ export PATH=$PATH:$SCALA_HOME/bin `
  - Check scala version: `$ scala -version`

Mac OSX users can get scala as indicated [here](https://medium.com/@djamaldg/how-to-install-scala-on-macos-5771d55339cb)


## Download and test Spark:

Unix users can get Spark as indicated below:

  - Get sources:`$ wget https://www.apache.org/dyn/closer.lua/spark/spark-3.2.0/spark-3.2.0-bin-hadoop3.2.tgz`
  - Unzip sources: `$ tar xzvf spark-3.2.0-bin-hadoop3.2.tgz`
  - Move content into directory named spark: `$ mv spark-3.2.0-bin-hadoop3.2/ spark` 
  - Move such directory into /usr/local: `$ sudo mv spark/ /usr/local/`
  - Set env. variable: `$ export SPARK_HOME=/usr/local/spark`
  - Add to PATH: `$ export PATH=$PATH:SPARK_HOME/bin`
  - Launch Spark shell `$ spark-shell `
  - Close Spark shekk `$ :q `

WSL users can follow instructions [here](https://kontext.tech/column/spark/560/apache-spark-301-installation-on-linux-guide)

MacOSX users can follow instructions [here](https://www.tutorialkart.com/apache-spark/how-to-install-spark-on-mac-os/
<!-- Spark wordcount example video: https://www.youtube.com/watch?v=HQTB3hlLD6E -->)

## Note on versioning
The suggested version of Scala is 2.12.
The recommended version is to use Spark 3.2.0 (last release) pre-built for Apache Hadoop 3.3 and later.

## Run spark examples ([local mode](http://spark.apache.org/docs/latest/)):
Spark comes with several sample programs. Scala, Java, Python and R examples are in the `examples/src/main` directory. 
  - Scala: `$ run-example SparkPi 10`
  - Python (need standalone spark cluster running): `$ spark-submit examples/src/main/python/pi.py 10`

## Run spark example from spark-shell (Scala)
Now let's try and run the toy example from spark RDD slides
  - Run spark shell in local mode: `$ spark-shell`
  - Use scala code from slides:

```
[scala> val pets = sc.parallelize(List(("cat", 1), ("dog", 1), ("cat", 2)));
[scala> val pets2 = pets.reduceByKey((x, y) => x + y);
[scala> val pets3 = pets2.sortByKey();
[scala> pets3.saveAsTextFile("pet-output/");
[scala> :q
```
  - Verify output: `$ cat pet-output/part-0000 `
  
## Run Wordcount in local Standalone mode from Spark Shell (Scala)
 * Run Spark master: `$ sbin/start-master.sh`
 * Check Spark master UI on browser at `localhost:8080`
 * Run Spark slave: `$ sbin/start-slave.sh <HOST:PORT> `
 * Locate a textfile in your Spark home directory (e.g. README.md)
 * Launch interactive spark shell, using the master in local mode, with 4 threads for wordcount: `$ spark-shell --master "local[4]" `
 * Use Scala code for wordcount:

 ```
 [scala> var map = sc.textFile("README.md").flatMap(line => line.split(" ")).map(word => (word,1));
 [scala> var counts = map.reduceByKey(_+_);
 [scala> counts.saveAsTextFile("output/");
 [scala> :q
```
 * Verify output: `$ cat output/part-0000 `
 * Run Wordcount in same mode but in Python as illustrated [here](https://www.tutorialkart.com/apache-spark/python-spark-shell-pyspark-example/)
 * Note 1: use `$ quit()` to exit the pyspark shell
 * Note 2: pyspark works with versions up to python 3.7, not supported in python 3.8 
 * Run another example with pyspark [here](https://spark.apache.org/docs/latest/quick-start.html#basics)

See also example [here](https://www.tutorialkart.com/apache-spark/scala-spark-shell-example/)

### Note: Local vs Standalone Spark cluster 
We have said you can run Spark locally or on a distributed file system (Hadoop). Even when you are running spark locally (without Hadoop cluster running), you can either run it without a cluster (like when we run scala and python examples) or on standalone cluster mode, using spark cluster and no distributed file system. In this case (which is necessary for running examples such as wordcount) you need to launch the spark master and slave locally.



## Running SPARK from your Java/Python program
 * Follow the simple example for self-contained application [here](https://spark.apache.org/docs/latest/quick-start.html#basics).
 * Note: the examples are using SparkSession instead of SparkContext. SparkSession (also available from the spark shell) unifies all Spark functionalities (SparkSQL, SparStreaming, ...) including those available in SparkContext (SparkCore). It prevents you from having to create different SparkContext for different groups of functionalities.

## Additional links, blogs, resources (this is a fast evolving section)
 * [Hadoop and Spark common errors, April 2020](https://medium.com/analytics-vidhya/9-issues-ive-encountered-when-setting-up-a-hadoop-spark-cluster-for-the-first-time-87b023624a43)
