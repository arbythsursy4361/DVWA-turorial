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
    <td>項次</td>
    <td>品名</td>
    <td>描述</td>
  </tr>
  <tr>
    <td>1</td>
    <td>iPhone 5</td>
    <td>iPhone 5是由蘋果公司開發的觸控式螢幕智慧型手機，是第六代的iPhone和繼承前一代的iPhone 4S。這款手機的設計比較以前產品更薄、更輕，及擁有更高解析度及更廣闊的4英寸觸控式螢幕，支援16:9寬螢幕。這款手機包括了一個自定義設計的ARMv7處理器的蘋果A6的更新、iOS 6操作系統，並且支援高速LTE網路。</td>
  </tr>
</table>
