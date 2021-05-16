## 错误提示语

nextcloud 您的数据目录可被其他用户读取 请更改权限为 0770 以避免其他用户查看目录.

## 解决办法

config.php 添加

```php
'check_data_directory_permissions' => false
```

Copy

 /nextcloud/config/config.php