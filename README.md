# Apache Spark
This lab will introduce the basics of Spark and guide you through installing and running spark via commandline as well as from within Java.

* Download and test Scala:
  - `$ wget ...`
  - `$ tar ... `
  - `$ scalac -version`

* Download and test Spark:
  - `$ wget ...`
  - `$ tar ... `
  - Launch Spark shell `$ spark-shell `
  - Close Spark shekk `$ :q `


* Run spark examples:
  - Scala:
  - Python:
  
## Run Wordcount in local Standalone mode from Spark Shell
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


## Note: Run spark master
Even when you are running spark on local mode (without Hadoop cluster running), you need to launch the spark master with the following command from the spark main directory:
  - `$ sbin/start-master.sh`


[Linux/Unix](https://medium.com/@djamaldg/how-to-install-scala-on-macos-5771d55339cb)
<!--MAC OS X
https://www.tutorialkart.com/apache-spark/how-to-install-spark-on-mac-os/-->


