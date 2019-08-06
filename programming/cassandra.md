# Cassandra

## Setup

Pull and run as a Docker instance:

```bash
$ docker pull cassandra
$ docker run --name cassandra -p 127.0.0.1:9042:9042 -p 127.0.0.1:9160:9160  -d cassandra:latest
```

Run commands inside the container:

```bash
$ docker exec -it cassandra bash
```

Logs

```bash
$ docker logs some-cassandra
```

## First Steps

```bash
$ docker exec -it cassandra bash
root@:/# cqlsh
cqlsh >
```

Create a namespace that will store the tables;

```cql
> CREATE KEYSPACE mydb WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 1 };
> use mydb;
```

Create a table;
```cql
mydb> CREATE TABLE books (id int PRIMARY KEY, title text, year text);
```

Describe a table;

```cql
mydb> DESC books;

CREATE TABLE mydb.books (
    id int PRIMARY KEY,
    title text,
    year text
) WITH bloom_filter_fp_chance = 0.01
    AND caching = {'keys': 'ALL', 'rows_per_partition': 'NONE'}
    AND comment = ''
    AND compaction = {'class': 'org.apache.cassandra.db.compaction.SizeTieredCompactionStrategy', 'max_threshold': '32', 'min_threshold': '4'}
    AND compression = {'chunk_length_in_kb': '64', 'class': 'org.apache.cassandra.io.compress.LZ4Compressor'}
    AND crc_check_chance = 1.0
    AND dclocal_read_repair_chance = 0.1
    AND default_time_to_live = 0
    AND gc_grace_seconds = 864000
    AND max_index_interval = 2048
    AND memtable_flush_period_in_ms = 0
    AND min_index_interval = 128
    AND read_repair_chance = 0.0
    AND speculative_retry = '99PERCENTILE';

mydb>
```