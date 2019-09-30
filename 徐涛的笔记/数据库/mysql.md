# mysql


## 常见操作sql语句
[databaseRecord.txt](_v_attachments/20190926100934108_23771/databaseRecord.txt)
### 增加表的一条数据

```sql

insert into `tm_fix_code` (`CODE_TYPE`, `CODE`, `CODE_NAME`, `REMARK`, `CREATE_DATE`, `CREATE_BY`, `UPDATE_DATE`, `UPDATE_BY`, `VER`) values('2102','21021002','业务内勤审核','车抵贷进件审核状态','2019-09-26 10:00:05',NULL,'2019-09-26 10:00:08',NULL,'1');

```
### 增加几个字段在哪个后面

```sql

ALTER TABLE `hxmotor`.`tm_dealer_file` ADD COLUMN `dealer_status` INT(8) NULL COMMENT '备案状态：已备案、未备案;2081' AFTER `ver`, ADD COLUMN `start_date` DATETIME NULL COMMENT '生效开始日期' AFTER `dealer_status`, ADD COLUMN `end_date` DATETIME NULL COMMENT '生效结束日期' AFTER `start_date`, ADD COLUMN `status` INT(8) DEFAULT 10011001 NULL COMMENT '状态：有效、无效' AFTER `end_date`;


```
### 更新具体某个数据值

```sql

UPDATE tm_fix_code 
SET 
    CODE_NAME = '调额专员审核'
WHERE
   CODE = '20861002';






实例：

更新了员工编号1056的姓氏和电子邮件列：
UPDATE employees 
SET 
    lastname = 'Hill',
    email = 'mary.hill@yiibai.com'
WHERE
    employeeNumber = 1056;


```




### 根据条件更新表里面的数据

```sql

UPDATE tt_finance_account a SET a.refund_date = 
(SELECT MAX(b.APPROVAL_DATE) FROM tt_finance_appauthitem b WHERE a.finance_id= b.finance_id
	AND b.APPROVAL_RESULT='20711014'
)
WHERE a.`status` = 20711014;

```

### 根据条件删除某条数据

```sql

插入一条数据：

insert into h5user (opid,mccode,teacct,paydate,querydate,remarks,enable,withholding_flag) values('o_XOw1bc51n3j1CyXmUIWguAnsO4','000536','12345678','20170731','28','test','1','0');

删除刚刚插入的数据：
delete from h5user where opid = 'o_XOw1bc51n3j1CyXmUIWguAnsO4';


--删除离职用户的相关信息
select * from tm_user a where a.REAL_NAME in ('陈舒松','张云','张涛');
delete from tm_position_user  where exists (select 1 from tm_user b where tm_position_user.USER_ID= b.USER_ID and b.USER_STATUS=10011002)





```



## SQL逻辑查询语句执行顺序[链接](https://www.cnblogs.com/wangfengming/articles/7880312.html)


## MySQL数据查询之多表查询[链接](https://www.cnblogs.com/bypp/p/8618382.html)

## mysql字符操作
### 字符串拼接
CONCAT(LEFT('我爱你',2),'-01')

### mysql 格式化字符串长度不够补0[链接](https://blog.csdn.net/yuhui123999/article/details/79126862)
```
LPAD(str,len,padstr) 返回字符串 str, 其左边由字符串padstr 填补到len 字符长度。假如str 的长度大于len, 则返回值被缩短至 len 字符。

select LPAD('1', 8, 0)

```

## mysql日期操作
<pre>
时间转字符串
select date_format(now(), '%Y-%m-%d');  

#结果：2017-01-05  


字符串转时间
select str_to_date('2016-01-02', '%Y-%m-%d %H');  

#结果：2017-01-02 00:00:00  
</pre>


### 相隔月数的计算(跨月就算一次，不按天算)
> 例子：今天距指定时间间隔月份
```sql
 SELECT TIMESTAMPDIFF(
    MONTH,
    STR_TO_DATE(CONCAT(LEFT(DATE_FORMAT(NOW(), '%Y-%m-%d'),7),"-01"),'%Y-%m-%d'),
    STR_TO_DATE(CONCAT(LEFT('2019-09-01',7),"-01"), '%Y-%m-%d')
  )
```


```sql
 (TIMESTAMPDIFF(
    MONTH,
    STR_TO_DATE(CONCAT(LEFT(xei.entry_date,7),'-01'), '%Y-%m-%d'),
    STR_TO_DATE(CONCAT(LEFT(childSelect.nowTime,7),'-01'), '%Y-%m-%d')
  )-1)  pureMonth,
  
```
### 相隔月数的计算(按天算)[链接](https://blog.csdn.net/jiahao1186/article/details/82586889)
```sql
SELECT
  NOW() 当前日期,
  DATE_ADD(NOW(), INTERVAL - 400 DAY) 历史日期,
  TIMESTAMPDIFF(
    MONTH,
    DATE_ADD(NOW(), INTERVAL - 400 DAY),
    NOW()
  ) AS 相差月;
 ———————————————— 
版权声明：本文为CSDN博主「春风化作秋雨」的原创文章，遵循CC 4.0 by-sa版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/jiahao1186/article/details/82586889
```

### mysql 保留两位小数[链接](https://www.cnblogs.com/xiaomai333/p/7647381.html)
> 1、round(x,d) :用于数据的四舍五入,round(x)  ,其实就是round(x,0),也就是默认d为0；
这里有个值得注意的地方是，d可以是负数，这时是指定小数点左边的d位整数位为0,同时小数位均为0；
SELECT ROUND(100.3465,2),ROUND(100,2),ROUND(0.6,2),ROUND(114.6,-1);
结果分别：100.35,100，0.6,110


### mysql基本函数示例

#### DATE_FORMAT(date,format)函数则是把数据库的日期转换为对应的字符串格式，比较常见，不做解释。
```sql

DATE_FORMAT(xei.entry_date, '%Y-%m-%d')

```

#### STR_TO_DATE(str,format)函数是将时间格式的字符串（str），按照所提供的显示格式（format）转换为DATETIME类型的值。
```sql

STR_TO_DATE(
  DATE_FORMAT(xei.entry_date, '%Y-%m-%d'),
  '%Y-%m-%d'
),

```



#### 时间差函数TIMESTAMPDIFF、DATEDIFF的用法

```sql

  DATE_FORMAT('2019-09-12','%Y-%m-%d') nowTime


  TIMESTAMPDIFF(
    MONTH,
    STR_TO_DATE(
      DATE_FORMAT(xei.entry_date, '%Y-%m-%d'),
      '%Y-%m-%d'
    ),
    STR_TO_DATE(childSelect.nowTime, '%Y-%m-%d')
  ) serviceTimeOfMonth,
  
```

#### 字符串拼接
```sql
CONCAT(LEFT('我爱你',2),'-01')
```

#### if
```sql
if(recurit_approval=20511001,'✔','')  recurit_approval
```

#### case when  枚举这个字段所有可能的值
```sql
SELECT
	NAME '英雄',
	CASE NAME
		WHEN '德莱文' THEN
			'斧子'
		WHEN '德玛西亚-盖伦' THEN
			'大宝剑'
		WHEN '暗夜猎手-VN' THEN
			'弩'
		ELSE
			'无'
	END '装备'
FROM
	user_info;
————————————————
版权声明：本文为CSDN博主「p7+」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_30038111/article/details/79611167


SELECT
	NAME '英雄',
	age '年龄',
	CASE
		WHEN age < 18 THEN
			'少年'
		WHEN age < 30 THEN
			'青年'
		WHEN age >= 30
		AND age < 50 THEN
			'中年'
		ELSE
			'老年'
	END '状态'
FROM
	user_info;
————————————————
版权声明：本文为CSDN博主「p7+」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_30038111/article/details/79611167

```

#### 聚合函数 sum 配合 case when 的简单函数实现多表 left join 的行转列

```sql
SELECT
	st.stu_id '学号',
	st.stu_name '姓名',
	sum(
		CASE co.course_name
		WHEN '大学语文' THEN
			sc.scores
		ELSE
			0
		END
	) '大学语文',
	sum(
		CASE co.course_name
		WHEN '新视野英语' THEN
			sc.scores
		ELSE
			0
		END
	) '新视野英语',
	sum(
		CASE co.course_name
		WHEN '离散数学' THEN
			sc.scores
		ELSE
			0
		END
	) '离散数学',
	sum(
		CASE co.course_name
		WHEN '概率论与数理统计' THEN
			sc.scores
		ELSE
			0
		END
	) '概率论与数理统计',
	sum(
		CASE co.course_name
		WHEN '线性代数' THEN
			sc.scores
		ELSE
			0
		END
	) '线性代数',
	sum(
		CASE co.course_name
		WHEN '高等数学' THEN
			sc.scores
		ELSE
			0
		END
	) '高等数学'
FROM
	edu_student st
LEFT JOIN edu_score sc ON st.stu_id = sc.stu_id
LEFT JOIN edu_courses co ON co.course_no = sc.course_no
GROUP BY
	st.stu_id
ORDER BY
	NULL;
————————————————
版权声明：本文为CSDN博主「p7+」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_30038111/article/details/79611167



统计为null的写法 和 sum的加法

[参考](https://www.cnblogs.com/xp796/p/8042100.html)

-- 统计男女性别
 SELECT
COUNT(1) 总人数 
 ,
  SUM(
    CASE
      gender
      WHEN 10061001
      THEN 1
      ELSE 0
    END
  ) '男',
  SUM(
    CASE
      gender
      WHEN 10061002
      THEN 1
      ELSE 0
    END
  ) '女',
  SUM(
    CASE
      gender IS NULL
      WHEN TRUE 
      
      THEN 1
      ELSE 0
    END
  ) +
  SUM(
    CASE
      gender 
      WHEN 10061003 
      
      THEN 1
      ELSE 0
    END
  ) 
  
  '未知'
FROM
  `xz_employee_info`
WHERE is_job = "是"




```
#### 日期推后一个月
```sql
SELECT DATE_ADD(NOW(),INTERVAL 1 MONTH) 
```


### 子查询的统一参数的实现
```sql
SELECT 
t.startDate 开始日期,
t.endDate 结束日期,
  TIMESTAMPDIFF(
    MONTH,
    STR_TO_DATE(t.startDate, '%Y-%m-%d'),
    STR_TO_DATE(t.endDate, '%Y-%m-%d')
  ) AS 相隔月数,
  IF(RIGHT(t.startDate,2)>RIGHT(t.endDate,2),TIMESTAMPDIFF(
    DAY,
    STR_TO_DATE(CONCAT(LEFT(DATE_ADD(t.endDate,INTERVAL -1 MONTH),7),'-',RIGHT(t.startDate,2) ), '%Y-%m-%d'),
    STR_TO_DATE(t.endDate, '%Y-%m-%d')
  ),RIGHT(t.endDate,2)-RIGHT(t.startDate,2)) 多余天数
  
  FROM (SELECT
    '2018-12-28' startDate,
    '2019-04-01' endDate) t
```

### mysql统计年龄

```sql


年龄：默认离职的不考虑在内
	此刻在职人数：（统计是否在职字段为是）
	建议分年龄段统计，10岁为一个阶段。
	18~28岁人数
	28-38岁人数
	...

SELECT
  NAME,
  COUNT(NAME) AS VALUE
FROM
  (SELECT
    CASE
      WHEN age < 20
      THEN '19岁及以下'
      WHEN age <= 29
      THEN '20-29岁'
      WHEN age <= 39
      THEN '30-39岁'
      WHEN age <= 49
      THEN '40-49岁'
      WHEN age <= 59
      THEN '50-59岁'
      ELSE '60岁及以上'
    END AS NAME
  FROM
    (
    SELECT
      TIMESTAMPDIFF(YEAR,ry.birth_date ,CURDATE())AS age
    FROM
      `xz_employee_info` ry
    WHERE ry.birth_date IS NOT NULL AND ry.is_job='是')t )t
    GROUP BY NAME
```