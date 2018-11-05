

## 1 用Java从Excel导数据到Mysql

* 步骤
    * 在Mysql数据库中先建好table
    * 从Excel表格读数据
    * 用JDBC连接Mysql数据库
    * 把读出的数据导入到Mysql数据库的相应表中

## 2 数据预处理
* ***previous***<br>
	DataImport,Procedures,InitSQL,ConnectMySQL,Main  
* ***2018.10.29***<br>
	添加DataExport.java，查询数据结果返回一个String[]，这样就可以输出到图结构中了。
* ***2018.11.01***<br>
	今天对数据认真研究了一下，各种各样的无效数据啊，我先分类汇总一下，最后再决定怎么筛选数据。
	`dataclean.md`,	`all.sql`,linux下的mysql workbench真的很不好用,很多语句在win10运行没问题的，
	在Linux就是不行，看来是mysql的问题。后面还是尽量用win10来做吧。
* ***2018.11.04***<br>
	继续分析数据，对`tbl_call`去重，主要内容在`20181104.sql`，新建数据表`tbl_serv_no`存放服务号码的通话数据。
	有效数据量66864.
* ***2018.11.05***<br>
	之前的分析还是有遗漏，一是95开头的，二是931开头的。看样子95开头的都是服务号码，而931开头的号码却很奇怪。
	931是兰州的区号。931开头的号码有5337个，其中5335个是短消息，8位，比如93100120,93100038，并且都是93100开头。
	剩下两个是CDMA，应该是电话，需要保留在tbl_call。或者，搞不清楚931开头的号码是什么，就先全部保留着。
	另外，在win10下，存储过程的名字存放的表名不同，那判断存储过程存不存在的SQL语句就没办法统一了。
	实在不行的话，存储过程存在就先删除再创建，这样每次导数据就得创建存储过程。不过应该也耗费不了多少时间。
	* 今天继续做了根据筛选条件提取数据，这部分也不难。在DataFetch.java里。跟DataExport一样，返回String[]就行了。
	至于细节方面，比如要查询哪些数据，根据哪些筛选条件，可以再做修改。框架有了就好做了。
	那么，好像工作完成的差不多了，明天正好汇报，看接下来还需要做什么。
