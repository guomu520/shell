# grep 查找字符串
grep [OPTION]... PATTERN [FILE]...

## 1、-w（--word-regexp）、-l（--file-with-matches）、-n（--line-number）、-v（--invert-match）
```bash
$ grep -r "yongfeimiao" .
./test1/1.txt:yongfeimiao
./a.txt:yongfeimiao
./a.txt:yongfeimiao1
./a.txt:yongfeimiao3

$ grep -rw "yongfeimiao" .
./test1/1.txt:yongfeimiao
./a.txt:yongfeimiao

$ grep -rl "yongfeimiao" .
./test1/1.txt
./a.txt

$ grep -rn "yongfeimiao" .
./test1/1.txt:1:yongfeimiao
./a.txt:1:yongfeimiao
./a.txt:2:yongfeimiao1
./a.txt:3:yongfeimiao3

$ grep -c "yongfeimiao" a.txt
3

$ grep -wv "yongfeimiao" a.txt
yongfeimiao1
yongfeimiao3
```

## 2、-B（--before-content=NUM）、-A（--after-content=NUM）、-C（--content=NUM）
```bash
$ grep '2015-11-17 15:45:59' /home/work/webdata/logs/db_log
[2015-11-17 15:45:59]	Array

#当前行前面NUM行，NUM数不含当前行
$ grep '2015-11-17 15:45:59' -B 3 /home/work/webdata/logs/db_log
)


[2015-11-17 15:45:59]	Array

#当前行后面NUM行，NUM数不含当前行
$ grep '2015-11-17 15:45:59' -A 3 /home/work/webdata/logs/db_log
[2015-11-17 15:45:59]	Array
(
    [message] => Passed variable is not an array or object, using empty array instead
    [url] => http://goods.mlservice.yongfeimiao.rdlab.meilishuo.com/goods/goods_sale_num_add?goods_id=77432291&sale_num=10

#当前行前后各NUM行，NUM数不含当前行
$ grep '2015-11-17 15:45:59' -C 3 /home/work/webdata/logs/db_log
)


[2015-11-17 15:45:59]	Array
(
    [message] => Passed variable is not an array or object, using empty array instead
    [url] => http://goods.mlservice.yongfeimiao.rdlab.meilishuo.com/goods/goods_sale_num_add?goods_id=77432291&sale_num=10

$ grep '2015-11-17 15:45:59' -3 /home/work/webdata/logs/db_log
)


[2015-11-17 15:45:59]	Array
(
    [message] => Passed variable is not an array or object, using empty array instead
    [url] => http://goods.mlservice.yongfeimiao.rdlab.meilishuo.com/goods/goods_sale_num_add?goods_id=77432291&sale_num=10
```

## 3、-P（--perl-regexp）、-o（--only-matching）
```bash
$ tail -2 phplibmqproxy.2015111814
[2015-11-18 14:50:52]	[publish_message]	INFO	{"endpoint":"http:\/\/127.0.0.1:9090\/produce?format=json","topic":"goods_other_topic","partition_key":"yongfeimiao.rdlab117362","message":{"_log_id":"yongfeimiao.rdlab117362","_topic":"goods_other_topic","_msg_key":"update_sph_goods","_partition_key":"yongfeimiao.rdlab117362","_consumer":"Mlservice\\Package\\Consumer\\Update_sph_goods\\SyncUpdateSphGoods","_retry_times":0,"_flag":"kafka","_data":"{\"type\":\"updateGoodsInfoSph\",\"goods_id\":[\"323\"],\"shop_id\":[],\"current_data\":\"a\"}"},"partition":5,"offset":0,"exception":"","timecost":"8.58","current_retry_time":0}
[2015-11-18 14:50:58]	[publish_message]	INFO	{"endpoint":"http:\/\/127.0.0.1:9090\/produce?format=json","topic":"goods_other_topic","partition_key":"yongfeimiao.rdlab117364","message":{"_log_id":"yongfeimiao.rdlab117364","_topic":"goods_other_topic","_msg_key":"update_sph_goods","_partition_key":"yongfeimiao.rdlab117364","_consumer":"Mlservice\\Package\\Consumer\\Update_sph_goods\\SyncUpdateSphGoods","_retry_times":0,"_flag":"kafka","_data":"{\"type\":\"updateGoodsInfoSph\",\"goods_id\":[\"323\"],\"shop_id\":[],\"current_data\":\"a\"}"},"partition":3,"offset":0,"exception":"","timecost":"5.73","current_retry_time":0}

$ tail -2 phplibmqproxy.2015111814 | grep -Po '"timecost":"[\d|\.]+'
"timecost":"8.58
"timecost":"5.73
```


