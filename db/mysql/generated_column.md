# カラムに式を定義する

## 姓・名からフルネームを生成するカラムを定義する例

### テーブル構造

```sql
CREATE TABLE TestTable(
  id INT PRIMARY KEY AUTO_INCREMENT,
  family_name VARCHAR(100),
  given_name VARCHAR(100),
  full_name VARCHAR(200) AS (CONCAT(family_name, given_name)) STORED
) CHARSET "utf8mb4";
```

### データ投入

```sql
INSERT INTO TestTable(family_name, given_name) VALUES("山田", "太郎");
```

full_name カラムには直接値を格納しない

### クエリ実行

```sql
SELECT * FROM TestTable
```

| id  | family_name | given_name | full_name |
| --- | ----------- | ---------- | --------- |
| 1   | 山田        | 太郎        | 山田太郎   |
