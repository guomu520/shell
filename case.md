#综合用例
**用例一：**
```bash
$ cat /home/service/nginx/logs/goods.mlservice.access.2016032215.log | grep '/goods/' | awk '{print $6}'| awk '{split($0,res,"?"); print res[1];}' | sort |uniq -c |sort -nr
 160043 /goods/goods_info
  42297 /goods/campaign_info
   4019 /goods/query_goods_sph
   2703 /goods/goods_status_update_sys
   1901 /goods/goods_sale_num_add
    936 /goods/Goods_expected_read
    692 /goods/query_goods
    640 /goods/cargo_info
    516 /goods/goods_save
    356 /shop/shop_set_and_can_goods_window_info
    133 /goods/goods_status
    113 /shop/shop_update_goods_window
    103 /goods/Goods_info
     52 /goods/goods_sph_update
      7 /goods/sku_info
      7 /goods/goods_status_update
      5 /goods/Goods_expected_set
      1 /goods/perhour_new_goods_num_set
      1 /goods/Goods_sph_update
      1 /consumer/consumer_proxy
      
$ cat /home/service/nginx/logs/goods.mlservice.access.2016032215.log | grep '/goods/' | awk -F ']' '{print $4}'|awk '{print $2}' | awk -F'?' '{print $1}' | sort |uniq -c |sort -nr | head -5
 160043 /goods/goods_info
  42297 /goods/campaign_info
   4019 /goods/query_goods_sph
   2703 /goods/goods_status_update_sys
   1901 /goods/goods_sale_num_add
```

**用例二：** 
使用awk,wc,sort,uniq,grep对nginx日志进行分析和统计
```bash
[rd@dfz-nx-01 ~]$ while [ true ];
do 
f=$(date +%Y%m%d%H);
t=$(date -d '-1 seconds' +%H:%M:%S);
x=$(grep $t /home/service/nginx/logs/goods.mlservice.access.$f.log | wc -l);
y=$(grep $t /home/service/nginx/logs/partner.mlservice.access.$f.log | wc -l);
echo $t" ——> qps="$(( ($y+$x)*6)) ;sleep 1; done
17:15:55 ——> qps=576
17:15:56 ——> qps=510
17:15:57 ——> qps=486
17:15:58 ——> qps=618
17:15:59 ——> qps=528
```

**用例三：**

```bash
$cat /home/work/webdata/logs/web/shop_cookie_maybe_stolen/shop_cookie_maybe_stolen_current

	[2015-12-08 23:57:23]	shop_id=114165 ，user_id=39827912 ，当前=（ip=202.99.196.175 ,city=太原市） ，登录时=（ip=183.60.183.7 ,city=广州市） ，访问页面=/manage/punish/{{item}} 。当前访问IP（城市）与登录时候不一致，疑似cookie被盗取	[dfz-bizsnake-04.meilishuo.com]	[10.5.13.76]
	
	[2015-12-08 23:57:41]	shop_id=114165 ，user_id=39827912 ，当前=（ip=202.99.196.175 ,city=太原市） ，登录时=（ip=183.60.183.7 ,city=广州市） ，访问页面=/manage/punish/

$cat /home/work/webdata/logs/web/shop_cookie_maybe_stolen/shop_cookie_maybe_stolen_current | grep -Po '当前=（ip=\d+\.\d+\.\d+\.\d+'

	当前=（ip=115.238.231.74
	当前=（ip=112.21.83.48
	当前=（ip=115.238.231.74
	当前=（ip=112.90.237.77
	当前=（ip=183.60.183.9
	当前=（ip=121.12.105.170

$cat /home/work/webdata/logs/web/shop_cookie_maybe_stolen/shop_cookie_maybe_stolen_current | grep -Po '当前=（ip=\d+\.\d+\.\d+\.\d+' | awk -F '=' '{print $3}'

	115.238.231.74
	183.60.183.1
	115.238.231.74
	183.60.183.7
	112.5.236.127
	121.12.105.170

$cat /home/work/webdata/logs/web/shop_cookie_maybe_stolen/shop_cookie_maybe_stolen_current | grep -Po '当前=（ip=\d+\.\d+\.\d+\.\d+' | awk -F '=' '{print $3}' | sort | uniq -c

      6 61.174.54.7
     87 61.174.54.8
     43 61.174.54.9
      1 61.184.160.60
      1 61.190.50.182
     12 61.52.64.131

$cat /home/work/webdata/logs/web/shop_cookie_maybe_stolen/shop_cookie_maybe_stolen_current | grep -Po '当前=（ip=\d+\.\d+\.\d+\.\d+' | awk -F '=' '{print $3}' | sort | uniq -c | 2 -n -k1,1

    532 121.12.105.134
    562 112.90.231.13
   1022 202.99.196.213
   3474 183.60.183.1
   3761 183.60.183.7
  20876 183.60.183.9
```
