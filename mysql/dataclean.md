数据清洗
====

## 总数据量是357882
## 1.根据对方号码字段的长度和号码类型筛选
`select count(*) from tbl_data where length(OppositePhoneNumber) = x;`

****当x=0,2,4时，result为0***

进一步查询语句为

`select OppositePhoneNumber from tbl_data where length(OppositePhoneNumber) = x and OppositePhoneNumber like '1%';`

|x|result|means|
|:-:|:-:|-|
|1|273115|对方号码数据为空，进一步查询发现，其中273114个为" ", 还有1个为"0"|
|3|3|110,122|
|5|4133|10086,51130,95580|
|6|834|100861,827004,966185|
|7|8219|7位的号码应该大部分是固定电话,少部分为服务号码,比如1008611,1183119|
|8|8102|8位的跟7位差不多，大部分是固话，也有服务号码，有2316个1开头的,如10655158|
|9|397|68个861186666这样的号码,其余全是1开头的服务号码|
|10|291|400、1065、111开头|
|11|60380|大部分为手机号|
|12|675|151个1065开头的，524个1069开头的|
|13|445|31个0开头的，可能为电话号码，其余为1065和1069|
|14|370|58个非1开头的，可能为电话号码或者网络电话,其余为1065/1069|
|15|313|3个00开头的，其余为1065/1069|
|16|320|全部为1开头,其中310个106开头|
|17|79|一个00881开头，其余为1065/1069|
|18|90|一个00952开头，其余为1065/1069|
|19|96|全部为1065/1069|
|20|20|6个95572开头的,其余为1065/1069|


## 2.根据通话记录类型筛选
sql语句见dataProcss/mysql/all.sql #20181101

|通话类型|count|备注|
|:-:|:-:|-|
|GPRS|271683|这部分数据量最大，但全部都是无效数据，因为这271683条数据中的对方号码都为空|
|GSM|33597||
|CDMA|10955||
|CDMA1X|1431|这部分也是空的。对方号码为空的数据就这两种(GPRS,CDMA1X)，还有一条为"0"的|
|短消息|40211||
|长途通信|5||

## 3.根据通话时间通话时长来筛选
通话日期、通话时间、通话时长 重复的数据共29658条
其中对方号码不为空的8363条
