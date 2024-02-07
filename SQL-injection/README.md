Low-level
---
通常 sql 語法會長這樣：sql = SELECT * FROM (tabel_name) WHERE (column_name) = '$id';

SQL injection 旨在正常的 sql 語法中執行惡意的 sql 語法來得到敏感資料(i.g. 帳號密碼...)。

Step 1.
---

可以更改上面 '$id' 的部分，改成：sql = SELECT * FROM (tabel_name) WHERE (column_name) = <font color = "red">'</font>'1' OR '1' = '1'<font color = "red">'</font>; <font color = "red">注意有時候會有'導致 query 失敗！</font>

因為 OR 的關係，導致該語法會 query 所有的使用者出來。
