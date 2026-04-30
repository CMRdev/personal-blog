# TSDB 操作

- taos;
- show databases;
- use idmp;
- show stables;
- show tables;

## 插入数据

- localhost:6060

```sql
insert into `idmp_sample_utility`.`em-1` (ts,`current`,`voltage`) values (now, 1.6, 210);
```

## 查询

- 现在查询 tag 信息和值的方式总共有三种：
  - show tags from 子表名
  - select \* from information_schema.ins_tags where
  - SELECT TAGS
- 在数据库中子表数量较大的时候（百万级）前两种方式的性能会变得非常差

## 运行 tsdb

```bash
docker run -d \
  -v ~/data/taos/dnode/data:/var/lib/taos \
  -v ~/data/taos/dnode/log:/var/log/taos \
  -p 6030:6030 -p 6041:6041 -p 6043:6043 -p 6060:6060 \
  -p 6044-6049:6044-6049 \
  -p 6044-6045:6044-6045/udp \
  --name tdengine-tsdb \
  tdengine/tsdb-ee-amd64:3.3.7.0
```
