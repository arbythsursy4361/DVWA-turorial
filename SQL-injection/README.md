Low-level
---
通常 sql 語法會長這樣：sql = SELECT * FROM (tabel_name) WHERE (column_name) = '$id';

SQL injection 旨在正常的 sql 語法中執行惡意的 sql 語法來得到敏感資料(i.g. 帳號密碼...)。

Step 1.
---

可以更改上面 '$id' 的部分，改成：1' OR 1 = 1; #

(p.s. 有時候會因為'導致 query 失敗，要注意！)

因為 OR 的關係，導致該語法會 query 所有的使用者出來。

Step 2.
---

由於我們會想知道更多資訊，會使用 UNION SELECT ... 去做二次查詢

因為 SELECT 出來的變數數量會被前台顯示限制住，所以可以會加入 group_concat(variable1, variable2, ...) 全部顯示出來。

因此可以將 '$id' 改成 UNION SELECT version(), database(); # 來查詢資料庫

Step 3.
---

MySQL 5.0 以上存在 information_schema，可以利用 information_schema 獲得資料庫進一步資訊

<table>
  <tr>
    <td>Column name</td>
    <td>Data type</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>TABLE_CATALOG</td>
    <td>nvarchar(128)</td>
    <td>Table qualifier.</td>
  </tr>
  <tr>
    <td>TABLE_SCHEMA</td>
    <td>nvarchar(128)</td>
    <td>Name of schema that contains the table.</td>
  </tr>
  <tr>
    <td>TABLE_NAME</td>
    <td>sysname</td>
    <td>Table name.</td>
  </tr>
  <tr>
    <td>TABLE_TYPE</td>
    <td>varchar(10)</td>
    <td>Type of table. Can be VIEW or BASE TABLE.</td>
  </tr>
</table>
