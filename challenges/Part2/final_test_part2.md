## Part2

#### Problem 1

select id, type, status, amount, (b.avg_amount-amount) difference
from problem1.account a,
(select avg(amount) avg_amount from account) b
where status = 'Active' ;

<pre><code>
[training@localhost ~]$ hive -f /home/training/problem1/solution.sql2019-06-19 00:28:06,367 WARN  [main] mapreduce.TableMapReduceUtil: The hbase-prefix-tree module jar containing PrefixTreeCodec is not present.  Continuing without it.

Logging initialized using configuration in file:/etc/hive/conf.dist/hive-log4j.properties
OK
Time taken: 0.613 seconds
Warning: Map Join MAPJOIN[16][bigTable=?] in task 'Stage-4:MAPRED' is a cross product
Query ID = training_20190619002828_64f83b6d-2fff-4158-b11e-65a9dfe6433e
Total jobs = 2
Launching Job 1 out of 2
Number of reduce tasks determined at compile time: 1
In order to change the average load for a reducer (in bytes):
  set hive.exec.reducers.bytes.per.reducer=<number>
In order to limit the maximum number of reducers:
  set hive.exec.reducers.max=<number>
In order to set a constant number of reducers:
  set mapreduce.job.reduces=<number>
Starting Job = job_1560916527501_0020, Tracking URL = http://localhost:8088/proxy/application_1560916527501_0020/
Kill Command = /usr/lib/hadoop/bin/hadoop job  -kill job_1560916527501_0020
Hadoop job information for Stage-1: number of mappers: 1; number of reducers: 1
2019-06-19 00:28:20,217 Stage-1 map = 0%,  reduce = 0%
2019-06-19 00:28:25,706 Stage-1 map = 100%,  reduce = 0%, Cumulative CPU 0.9 sec
2019-06-19 00:28:33,299 Stage-1 map = 100%,  reduce = 100%, Cumulative CPU 1.92 sec
MapReduce Total cumulative CPU time: 1 seconds 920 msec
Ended Job = job_1560916527501_0020
Execution log at: /tmp/training/training_20190619002828_64f83b6d-2fff-4158-b11e-65a9dfe6433e.log
2019-06-19 12:28:37	Starting to launch local task to process map join;	maximum memory = 1013645312
2019-06-19 12:28:39	Dump the side-table for tag: 0 with group count: 1 into file: file:/tmp/training/02fbcc66-be20-4ac4-a918-7e16f4e486fc/hive_2019-06-19_00-28-10_661_9216369902518425428-1/-local-10004/HashTable-Stage-4/MapJoin-mapfile00--.hashtable
2019-06-19 12:28:39	Uploaded 1 File to: file:/tmp/training/02fbcc66-be20-4ac4-a918-7e16f4e486fc/hive_2019-06-19_00-28-10_661_9216369902518425428-1/-local-10004/HashTable-Stage-4/MapJoin-mapfile00--.hashtable (2045 bytes)
2019-06-19 12:28:39	End of local task; Time Taken: 1.55 sec.
Execution completed successfully
MapredLocal task succeeded
Launching Job 2 out of 2
Number of reduce tasks is set to 0 since there's no reduce operator
Starting Job = job_1560916527501_0021, Tracking URL = http://localhost:8088/proxy/application_1560916527501_0021/
Kill Command = /usr/lib/hadoop/bin/hadoop job  -kill job_1560916527501_0021
Hadoop job information for Stage-4: number of mappers: 1; number of reducers: 0
2019-06-19 00:28:46,952 Stage-4 map = 0%,  reduce = 0%
2019-06-19 00:28:53,429 Stage-4 map = 100%,  reduce = 0%, Cumulative CPU 1.49 sec
MapReduce Total cumulative CPU time: 1 seconds 490 msec
Ended Job = job_1560916527501_0021
MapReduce Jobs Launched:
Stage-Stage-1: Map: 1  Reduce: 1   Cumulative CPU: 1.92 sec   HDFS Read: 9862 HDFS Write: 121 SUCCESS
Stage-Stage-4: Map: 1   Cumulative CPU: 1.49 sec   HDFS Read: 6097 HDFS Write: 3013 SUCCESS
Total MapReduce CPU Time Spent: 3 seconds 410 msec
OK
A100000	Basic Checking	Active	44539	5657.760000000002
A100002	Basic Checking	Active	11483	38713.76
A100003	Student Checking	Active	26132	24064.760000000002
A100007	Student Checking	Active	71661	-21464.239999999998
A100009	Savings	Active	65536	-15339.239999999998
A100010	Savings	Active	40778	9418.760000000002
A100011	Savings	Active	57953	-7756.239999999998
A100013	Basic Checking	Active	45654	4542.760000000002
A100016	Basic Checking	Active	639	49557.76
A100018	Basic Checking	Active	63563	-13366.239999999998
A100019	Basic Checking	Active	79771	-29574.239999999998
A100020	Basic Checking	Active	34328	15868.760000000002
A100021	Savings	Active	34405	15791.760000000002
A100022	Student Checking	Active	51850	-1653.239999999998
A100023	Basic Checking	Active	85337	-35140.24
A100025	Savings	Active	7265	42931.76
A100030	Student Checking	Active	7275	42921.76
A100032	Basic Checking	Active	51703	-1506.239999999998
A100033	Student Checking	Active	20139	30057.760000000002
A100034	Savings	Active	66835	-16638.239999999998
A100036	Savings	Active	1578	48618.76
A100037	Basic Checking	Active	98233	-48036.24
A100038	Savings	Active	4042	46154.76
A100040	Student Checking	Active	73539	-23342.239999999998
A100043	Student Checking	Active	86888	-36691.24
A100044	Basic Checking	Active	56530	-6333.239999999998
A100045	Student Checking	Active	44440	5756.760000000002
A100046	Savings	Active	17575	32621.760000000002
A100047	Savings	Active	94291	-44094.24
A100049	Savings	Active	98628	-48431.24
A100050	Savings	Active	99035	-48838.24
A100054	Savings	Active	86903	-36706.24
A100055	Savings	Active	61255	-11058.239999999998
A100056	Student Checking	Active	68404	-18207.239999999998
A100057	Basic Checking	Active	31550	18646.760000000002
A100058	Student Checking	Active	1189	49007.76
A100060	Student Checking	Active	35259	14937.760000000002
A100061	Basic Checking	Active	87322	-37125.24
A100062	Student Checking	Active	34025	16171.760000000002
A100067	Student Checking	Active	64871	-14674.239999999998
A100069	Basic Checking	Active	44071	6125.760000000002
A100071	Student Checking	Active	28357	21839.760000000002
A100073	Savings	Active	23589	26607.760000000002
A100074	Student Checking	Active	77169	-26972.239999999998
A100075	Basic Checking	Active	19327	30869.760000000002
A100076	Savings	Active	41747	8449.760000000002
A100078	Basic Checking	Active	78031	-27834.239999999998
A100079	Savings	Active	95810	-45613.24
A100082	Savings	Active	27664	22532.760000000002
A100083	Student Checking	Active	61306	-11109.239999999998
A100084	Savings	Active	69928	-19731.239999999998
A100086	Student Checking	Active	65928	-15731.239999999998
A100087	Savings	Active	19786	30410.760000000002
A100088	Basic Checking	Active	48954	1242.760000000002
A100089	Savings	Active	38086	12110.760000000002
A100091	Basic Checking	Active	66045	-15848.239999999998
A100094	Student Checking	Active	54444	-4247.239999999998
A100095	Basic Checking	Active	4212	45984.76
A100096	Student Checking	Active	82057	-31860.239999999998
A100098	Savings	Active	4139	46057.76
Time taken: 43.865 seconds, Fetched: 60 row(s)

</code></pre>


#### Problem 2

CREATE EXTERNAL TABLE employee (
id int,
fname string,
lname string,
address string,
city string,
state string,
zip string,
birthday string,
hireday string
)
ROW FORMAT SERDE 'parquet.hive.serde.ParquetHiveSerDe'
STORED AS
INPUTFORMAT "parquet.hive.DeprecatedParquetInputFormat"
OUTPUTFORMAT "parquet.hive.DeprecatedParquetOutputFormat"
LOCATION 'hdfs://localhost:8020/user/training/problem2/data/employee'
;

#### Problem 3

CREATE EXTERNAL TABLE solution (
id string,
fname string,
lname string,
hphone string
)
LOCATION 'hdfs://localhost:8020/user/training/problem3/data/solution'
;

insert overwrite table solution
select a.custid, b.fname, b.lname, b.hphone
from account a
left outer join customer b
where a.custid = b.id
and amount < 0;

select * from solution;

### Problem 4
CREATE EXTERNAL TABLE employee1 (
id string,
fname string,
lname string,
address string,
city string,
state string,
zip string
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t;'
LOCATION 'hdfs://localhost:8020/user/training/problem4/data/employee1'
;

CREATE EXTERNAL TABLE employee2 (
id string,
unknown string,
lname string,
fname string,
address string,
city string,
state string,
zip string
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
LOCATION 'hdfs://localhost:8020/user/training/problem4/data/employee2'
;

CREATE EXTERNAL TABLE solution (
id string,
fname string,
lname string,
address string,
city string,
state string,
zip string
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t;'
LOCATION 'hdfs://localhost:8020/user/training/problem4/solution'
;

insert overwrite table solution
select * from (
select id, initcap(fname), initcap(lname), address, city, state, substr(zip, 1, 5) as zip
from employee1 a where a.state = 'CA'
union all
select id, initcap(fname), initcap(lname), address, city, state, substr(zip, 1, 5) as zip
from employee2 b where b.state = 'CA'
) aa ;

### Problem 5

use problem5;

select c.fname, c.lname, c.city, c.state
from customer c
where c.state = 'CA'
and c.city = 'Palo Alto'
union all
select e.fname, e.lname, e.city, e.state
from employee e
where e.state = 'CA'
and e.city = 'Palo Alto';

<pre><code>
[training@localhost ~]$ hive -f /home/training/problem5/solution.sql
2019-06-19 00:24:58,950 WARN  [main] mapreduce.TableMapReduceUtil: The hbase-prefix-tree module jar containing PrefixTreeCodec is not present.  Continuing without it.

Logging initialized using configuration in file:/etc/hive/conf.dist/hive-log4j.properties
OK
Time taken: 0.782 seconds
Query ID = training_20190619002525_8109257a-4291-40f2-a0a1-b5974f6a3035
Total jobs = 1
Launching Job 1 out of 1
Number of reduce tasks is set to 0 since there's no reduce operator
Starting Job = job_1560916527501_0019, Tracking URL = http://localhost:8088/proxy/application_1560916527501_0019/
Kill Command = /usr/lib/hadoop/bin/hadoop job  -kill job_1560916527501_0019
Hadoop job information for Stage-1: number of mappers: 2; number of reducers: 0
2019-06-19 00:25:18,097 Stage-1 map = 0%,  reduce = 0%
2019-06-19 00:25:31,931 Stage-1 map = 100%,  reduce = 0%, Cumulative CPU 3.29 sec
MapReduce Total cumulative CPU time: 3 seconds 290 msec
Ended Job = job_1560916527501_0019
MapReduce Jobs Launched:
Stage-Stage-1: Map: 2   Cumulative CPU: 3.29 sec   HDFS Read: 23808 HDFS Write: 310 SUCCESS
Total MapReduce CPU Time Spent: 3 seconds 290 msec
OK
Farrah	Preston	Palo Alto	CA
Brielle	Hudson	Palo Alto	CA
Nelle	Kim	Palo Alto	CA
Tatum	Jacobs	Palo Alto	CA
Ivan	Gentry	Palo Alto	CA
Naida	Tran	Palo Alto	CA
Alden	Daniels	Palo Alto	CA
Maggy	Mcdaniel	Palo Alto	CA
Griffin	Pate	Palo Alto	CA
Burton	Hayes	Palo Alto	CA
Ali	Barker	Palo Alto	CA
Jasper	Lara	Palo Alto	CA
Time taken: 28.491 seconds, Fetched: 12 row(s)
</code></pre>

### Problem 6
Q6. There are privacy concerns about the employee data that is stored on the cluster. Your task is to remove any age information from the employee data by creating a new table for the data analysts to query against.

CREATE EXTERNAL TABLE problem6.solution(
id int,
fname string,
lname string,
address string,
city string,
state string,
zip string,
birthday string)
ROW FORMAT SERDE
'org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe'
WITH SERDEPROPERTIES (
'field.delim'='\t',
'serialization.format'='\t')
STORED AS INPUTFORMAT
'org.apache.hadoop.mapred.TextInputFormat'
OUTPUTFORMAT
'org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat'
LOCATION
'hdfs://localhost:8020/user/training/problem6/solution'
;

insert overwrite table problem6.solution
select id, fname, lname,address,city, state, zip, substr(birthday,1,5) birthday
from problem6.employee
;

select * from problem6.solution;

### Problem 7
Q7. Generate a report that contains all of the Seattle employee names in sorted order.

select concat(e.fname, ' ', e.lname) as name from employee e where e.city = 'Seattle' sort by name;

### Problem 8
Q8. Use Sqoop to export customer data from HDFS into a MySQL database table. Place the data in the solution table in MySQL, which has been created and is currently empty.

<pre><code>
[training@localhost ~]$ hive -f /home/training/problem1/solution.sql
2019-06-18 22:27:53,352 WARN  [main] mapreduce.TableMapReduceUtil: The hbase-prefix-tree module jar containing PrefixTreeCodec is not present.  Continuing without it.

Logging initialized using configuration in file:/etc/hive/conf.dist/hive-log4j.properties
FAILED: SemanticException [Error 10001]: Line 2:5 Table not found 'account'
[training@localhost ~]$ sqoop export --connect jdbc:mysql://localhost/problem8 --username cloudera --password cloudera --table solution --export-dir hdfs://localhost:8020/user/training/problem8/data/customer --input-fields-terminated-by '\t'
19/06/19 00:03:29 INFO sqoop.Sqoop: Running Sqoop version: 1.4.6-cdh5.8.0
19/06/19 00:03:29 WARN tool.BaseSqoopTool: Setting your password on the command-line is insecure. Consider using -P instead.
19/06/19 00:03:29 INFO manager.MySQLManager: Preparing to use a MySQL streaming resultset.
19/06/19 00:03:29 INFO tool.CodeGenTool: Beginning code generation
19/06/19 00:03:30 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `solution` AS t LIMIT 1
19/06/19 00:03:30 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `solution` AS t LIMIT 1
19/06/19 00:03:30 INFO orm.CompilationManager: HADOOP_MAPRED_HOME is /usr/lib/hadoop-mapreduce
Note: /tmp/sqoop-training/compile/3ffb09c51ae73295c6d32875de909d0c/solution.java uses or overrides a deprecated API.
Note: Recompile with -Xlint:deprecation for details.
19/06/19 00:03:33 INFO orm.CompilationManager: Writing jar file: /tmp/sqoop-training/compile/3ffb09c51ae73295c6d32875de909d0c/solution.jar
19/06/19 00:03:33 INFO mapreduce.ExportJobBase: Beginning export of solution
19/06/19 00:03:33 INFO Configuration.deprecation: mapred.job.tracker is deprecated. Instead, use mapreduce.jobtracker.address
19/06/19 00:03:33 INFO Configuration.deprecation: mapred.jar is deprecated. Instead, use mapreduce.job.jar
19/06/19 00:03:33 INFO Configuration.deprecation: mapred.map.max.attempts is deprecated. Instead, use mapreduce.map.maxattempts
19/06/19 00:03:34 INFO Configuration.deprecation: mapred.reduce.tasks.speculative.execution is deprecated. Instead, use mapreduce.reduce.speculative
19/06/19 00:03:35 INFO Configuration.deprecation: mapred.map.tasks.speculative.execution is deprecated. Instead, use mapreduce.map.speculative
19/06/19 00:03:35 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.maps
19/06/19 00:03:35 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032
19/06/19 00:03:36 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:830)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:826)
19/06/19 00:03:36 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/06/19 00:03:36 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:830)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:826)
19/06/19 00:03:36 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:830)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:826)
19/06/19 00:03:36 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:830)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:826)
19/06/19 00:03:36 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:830)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:826)
19/06/19 00:03:36 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/06/19 00:03:36 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:830)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:826)
19/06/19 00:03:36 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:830)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:826)
19/06/19 00:03:36 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/06/19 00:03:36 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/06/19 00:03:37 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/06/19 00:03:37 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:830)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:826)
19/06/19 00:03:37 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:830)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:826)
19/06/19 00:03:37 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/06/19 00:03:37 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:830)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:826)
19/06/19 00:03:37 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/06/19 00:03:37 INFO input.FileInputFormat: Total input paths to process : 1
19/06/19 00:03:37 INFO input.FileInputFormat: Total input paths to process : 1
19/06/19 00:03:37 WARN hdfs.DFSClient: Caught exception
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/06/19 00:03:37 INFO mapreduce.JobSubmitter: number of splits:4
19/06/19 00:03:37 INFO Configuration.deprecation: mapred.map.tasks.speculative.execution is deprecated. Instead, use mapreduce.map.speculative
19/06/19 00:03:37 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1560916527501_0015
19/06/19 00:03:38 INFO impl.YarnClientImpl: Submitted application application_1560916527501_0015
19/06/19 00:03:38 INFO mapreduce.Job: The url to track the job: http://localhost:8088/proxy/application_1560916527501_0015/
19/06/19 00:03:38 INFO mapreduce.Job: Running job: job_1560916527501_0015
19/06/19 00:03:47 INFO mapreduce.Job: Job job_1560916527501_0015 running in uber mode : false
19/06/19 00:03:47 INFO mapreduce.Job:  map 0% reduce 0%
19/06/19 00:04:05 INFO mapreduce.Job:  map 25% reduce 0%
19/06/19 00:04:06 INFO mapreduce.Job:  map 100% reduce 0%
19/06/19 00:04:06 INFO mapreduce.Job: Job job_1560916527501_0015 completed successfully
19/06/19 00:04:06 INFO mapreduce.Job: Counters: 30
	File System Counters
		FILE: Number of bytes read=0
		FILE: Number of bytes written=571200
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=18887
		HDFS: Number of bytes written=0
		HDFS: Number of read operations=19
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=0
	Job Counters
		Launched map tasks=4
		Data-local map tasks=4
		Total time spent by all maps in occupied slots (ms)=132688
		Total time spent by all reduces in occupied slots (ms)=0
		Total time spent by all map tasks (ms)=66344
		Total vcore-seconds taken by all map tasks=66344
		Total megabyte-seconds taken by all map tasks=33968128
	Map-Reduce Framework
		Map input records=100
		Map output records=100
		Input split bytes=676
		Spilled Records=0
		Failed Shuffles=0
		Merged Map outputs=0
		GC time elapsed (ms)=644
		CPU time spent (ms)=2270
		Physical memory (bytes) snapshot=458911744
		Virtual memory (bytes) snapshot=9048911872
		Total committed heap usage (bytes)=251920384
	File Input Format Counters
		Bytes Read=0
	File Output Format Counters
		Bytes Written=0
19/06/19 00:04:06 INFO mapreduce.ExportJobBase: Transferred 18.4443 KB in 31.8576 seconds (592.8576 bytes/sec)
19/06/19 00:04:06 INFO mapreduce.ExportJobBase: Exported 100 records.
</code></pre>

### Problem 9
Q9. Your company is being acquired by another company. To prepare for this acquisition, update the customer records to guarantee there will be no duplicate IDs with their existing customer IDs.

use problem9;

CREATE TABLE solution AS SELECT concat('A', '', id) as newId, fname, lname, address, city, state, zip, birthday FROM problem9.customer;

select * from problem9.solution;

### Problem 10
Q10. Your boss needs specialized reports using the billing data and is constantly asking for help to write SQL queries. Create a database view in the metastore so that your boss has customer and billing data joined.

use problem10;

create view solution as
select b.id as id, c.fname as fname, c.lname as lname, c.city as city, c.state as state, b.charge as charge, b.tstamp as billdata
from billing b
join customer c on (b.id = c.id);

select * from problem10.solution;

### Problem 11
Q11. Several analysis questions are described below and you will need to write the SQL code to answer them. You can use whichever tool you prefer? Impala or Hive ? using whichever method you like best, including shell, script, or the Hue Query Editor, to run your queries.

select count(o.order_id) as cnt, prod_id from order_details o group by o.prod_id order by cnt desc;
