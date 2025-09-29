# 既存のレコードの値から新しいレコードを作成する

```sql
INSERT INTO TableName (column1, column2, ...)
SELECT column1, column2, ...
FROM TableName
WHERE condition
```

## 最新レコードから新しいレコードを作成する例

### テーブル構造＆初期データ

```sql
CREATE TABLE TestTable(
  id INT PRIMARY KEY AUTO_INCREMENT,
  column1 VARCHAR(100),
  column2 VARCHAR(100)
);

INSERT INTO TestTable(column1, column2)
VALUES("r1c1", "r1c2"), ("r2c1", "r2c2");
```

### クエリ実行前のテーブル

| id  | column1 | column2 |
| --- | ------- | ------- |
| 1   | r1c1    | r1c2    |
| 2   | r2c1    | r2c2    |

### クエリ

```sql
INSERT INTO TestTable(column1, column2)
SELECT column1, column2
FROM TestTable
ORDER BY id DESC
LIMIT 1;
```

### クエリ実行後のテーブル

| id  | column1 | column2 |
| --- | ------- | ------- |
| 1   | r1c1    | r1c2    |
| 2   | r2c1    | r2c2    |
| 3   | r2c1    | r2c2    |
