# Azure VM start and stop: Azure の VM を起動・停止する

## パッケージのインストール

```sh
pip install azure-identity azure-mgmt-compute
```

## コード例

### 共通処理

```python
import os

from azure.identity import ClientSecretCredential
from azure.mgmt.compute import ComputeManagementClient

# サービスプリンシパルの情報
TENANT_ID = os.getenv("TENANT_ID")
CLIENT_ID = os.getenv("CLIENT_ID")
CLIENT_SECRET = os.getenv("CLIENT_SECRET")

# 対象のサブスクリプションのID
SUBSCRIPTION_ID = os.getenv("SUBSCRIPTION_ID")

# 対象のリソースグループ名
RESOURCE_GROUP_NAME = os.getenv("RESOURCE_GROUP_NAME")

# 対象の VM のリソース名
VM_NAME = os.getenv("VM_NAME")

# VM 操作のインスタンス生成
credentials = ClientSecretCredential(TENANT_ID, CLIENT_ID, CLIENT_SECRET)
compute_client = ComputeManagementClient(credentials, SUBSCRIPTION_ID)
virtual_machines_operation = compute_client.virtual_machines
```

### 起動

```python
poller = virtual_machines_operation.begin_start(RESOURCE_GROUP_NAME, VM_NAME)
poller.wait()
```

### 停止

```python
poller = virtual_machines_operation.begin_deallocate(RESOURCE_GROUP_NAME, VM_NAME)
poller.wait()
```

### 起動状態確認

```python
instance_view = virtual_machines_operation.instance_view(RESOURCE_GROUP_NAME, VM_NAME)
is_running = any(status.code == "PowerState/running" for status in instance_view.statuses)
```

## 参考

* [ClientSecretCredential Class](https://learn.microsoft.com/en-us/python/api/azure-identity/azure.identity.clientsecretcredential?view=azure-python)
* [ComputeManagementClient Class](https://learn.microsoft.com/en-us/python/api/azure-mgmt-compute/azure.mgmt.compute.computemanagementclient?view=azure-python)
