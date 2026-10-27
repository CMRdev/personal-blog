# TSDB 操作

- taos;
- show databases;
- use idmp;
- show stables;
- show tables;
- desc `vst_智能电表_784670`;

## 插入数据

- localhost:6060

```sql
insert into `idmp_sample_utility`.`em-1` (ts,`current`,`voltage`) values (now, 1.6, 210);
```

## 查询

```sql

select _c0, `电压` from `idmp`.`vt_em-1_azfmnf` where _c0 >= '2026-07-08';

-- "windowStart":1783493511326,"windowEnd":1783496511326
select cast(1783493511326 as timestamp) as winStart, cast(1783496511326 as timestamp) as winEnd;
select _c0, `电压` from `idmp`.`vt_em-1_azfmnf` where _c0 >= 1783493511326 and _c0 <= 1783496511326;
```

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
