# MapReduce WordCount Demo

这是一个基于 Maven 和 Hadoop 3.3.5 的 MapReduce WordCount 示例。

## 环境要求

- JDK 8
- Maven 3.9+
- Hadoop 3.3.5

## 获取项目

```bash
git clone https://github.com/JasonR-student/mapreduce-wordcount-demo.git
cd mapreduce-wordcount-demo
```

## 编译打包

```bash
mvn package
```

生成的可提交 JAR 文件：

```text
target/mapreduce-wordcount-demo-1.0-SNAPSHOT-jar-with-dependencies.jar
```

## 本地模式运行

本地模式不需要启动 HDFS：

```bash
rm -rf output_local
java -jar target/mapreduce-wordcount-demo-1.0-SNAPSHOT-jar-with-dependencies.jar \
  input.txt output_local --local
cat output_local/part-r-00000
```

## HDFS 集群运行

先启动 HDFS，并上传输入文件：

```bash
hdfs dfs -mkdir -p /user/hadoop/wordcount_input
hdfs dfs -put -f input.txt /user/hadoop/wordcount_input/
hdfs dfs -rm -r -f /user/hadoop/wordcount_output
```

提交 MapReduce 作业：

```bash
hadoop jar target/mapreduce-wordcount-demo-1.0-SNAPSHOT-jar-with-dependencies.jar \
  learn.hadoop.mapreduce.WordCount \
  /user/hadoop/wordcount_input \
  /user/hadoop/wordcount_output
```

查看结果：

```bash
hdfs dfs -cat /user/hadoop/wordcount_output/part-r-00000
```
