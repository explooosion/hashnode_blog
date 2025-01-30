---
title: "MSSQL - 全形與半形轉換"
seoTitle: "MSSQL - 全形與半形轉換"
seoDescription: "MSSQL 自訂函式 新手教學之 全形與半形轉換，請安心服用。"
datePublished: Fri May 27 2016 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbek0n000i0ajx9vj79jub
slug: mssql
tags: function

---

MSSQL 自訂函式 新手教學之 全形與半形轉換，請安心服用。

在 MSSQL中，若要進行資料全形半形轉換，可建立純量值函式

以下範例為轉載 [阿銓的異想世界](http://blog.xuite.net/chuimn/game/63620141-%5BMSSQL%5D%E5%85%A8%E5%BD%A2%E8%88%87%E5%8D%8A%E5%BD%A2%E8%BD%89%E6%8F%9B)：

建立函式
----

```sql
CREATE FUNCTION [dbo].[sConvert](
@str NVARCHAR(4000), --要轉換字串
@flag bit --0轉換成半形,1轉換成全形
)RETURNS Nvarchar(4000)
AS
BEGIN
DECLARE @chg Nvarchar(8),@step int,@i int
IF @flag=0
SELECT @chg=N'%[！-～]%',@step=-65248,
@str=REPLACE(@str,N'　 ',N' ')
ELSE
SELECT @chg=N'%[!-~]%',@step=65248,
@str=REPLACE(@str,N' ',N'　 ')
SET @i=PATINDEX(@chg COLLATE LATIN1_GENERAL_BIN,@str)
WHILE @i> 0
SELECT @str=REPLACE(@str,
SUBSTRING(@str,@i,1),
NCHAR(UNICODE(SUBSTRING(@str,@i,1))+@step))
,@i=PATINDEX(@chg COLLATE LATIN1_GENERAL_BIN,@str)
 
select @str = UPPER(@str)
RETURN(@str)
END
```

使用說明
----

```sql
SELECT dbo.sConvert([字串],[模式])
```

1.  0 為轉半形
2.  1為轉全形

有勘誤之處，不吝指教。ob'\_'ov