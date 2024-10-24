# azure data tables regist int64 value: Azure Table Storage に INT64 の値を登録する

## コード例

```py
from azure.data.tables import EdmType, EntityProperty, TableServiceClient

azure_storage_connection_string = "XXXXX"
table_service = TableServiceClient.from_connection_string(conn_str=azure_storage_connection_string)

table_name = "TestTable"
table_client = table_service.get_table_client(table_name=table_name)

values = {
  "PartitionKey": "INT64", 
  "RowKey": "INT64_VALUE", 
  "TestColumn": EntityProperty(2147483648, EdmType.INT64),
}
table_client.create_entity(values)
```

`EntityProperty` によって型を明示する。

## 型を明示しない場合

```py
from azure.data.tables import EdmType, EntityProperty, TableServiceClient

azure_storage_connection_string = "XXXXX"
table_service = TableServiceClient.from_connection_string(conn_str=azure_storage_connection_string)

table_name = "TestTable"
table_client = table_service.get_table_client(table_name=table_name)

# INT32 の値は型を明示しなくても登録可能
int32_values = {
  "PartitionKey": "INT32", 
  "RowKey": "INT32_VALUE", 
  "TestColumn": 2147483647,
}
table_client.create_entity(int32_values)

# INT64 の値は型を明示しないと TypeError が発生する
int64_values = {
  "PartitionKey": "INT32",
  "RowKey": "INT64_VALUE", 
  "TestColumn": 2147483648,
}
table_client.create_entity(int64_values)
# TypeError: 2147483648 is too large to be cast to type EdmType.INT32.
```

## 参考

* [EntityProperty クラス](https://learn.microsoft.com/ja-jp/python/api/azure-data-tables/azure.data.tables.entityproperty?view=azure-python)
* [EdmType 列挙型](https://learn.microsoft.com/ja-jp/python/api/azure-data-tables/azure.data.tables.edmtype?view=azure-python)
