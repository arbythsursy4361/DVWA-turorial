Low-level
---
通常 sql 語法會長這樣：sql = SELECT * FROM (tabel_name) WHERE (column_name) = '$id';\n
SQL injection 旨在正常的 sql 語法中執行惡意的 sql 語法來得到敏感資料(i.g. 帳號密碼...)。

Step 1.
---

可以更改上面 '$id' 的部分，改成：sql = SELECT * FROM (tabel_name) WHERE (column_name) = '1' OR '1' = '1';\n
(p.s. 有時候會因為'導致 query 失敗，要注意！)
因為 OR 的關係，導致該語法會 query 所有的使用者出來。

Step 2.
---

由於我們會想知道更多資訊，會使用 UNION SELECT ... 去做二次查詢

因為 SELECT 的數量會被系統顯示給限制，所以通常會加入 group_concat(variable1, variable2, ...) 去全部顯示。

