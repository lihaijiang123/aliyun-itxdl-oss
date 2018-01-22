
## 安装

安装有两种方式：

### ① 直接编辑配置文件

将以下内容增加到 composer.json：

```json
require: {
    "lihaijiang/aliyun-itxdl-oss": "~2.0"
}
```

然后运行 `composer update`。

### ② 执行命令安装

运行命令：

```bash
composer require lihaijiang/aliyun-itxdl-oss:~2.0
```

## 使用（以 Laravel 为例）

### 构建 Service 文件

新建 `app/services/OSS.php`，内容可参考：[OSS.php](aliyun-oss/src/oss/AliyunOSS.php)，然后修改配置：

```php
... ...

  private $city = '北京';

  private $networkType = '经典网络';
  
  private $AccessKeyId = '';
  private $AccessKeySecret = '';

... ...
```

### 放入自动加载

#### 遵循 psr-0 的项目（如Laravel 4、CodeIgniter、TinyLara）中：
在 `composer.json` 中 `autoload -> classmap` 处增加配置：

```json
"autoload": {
    "classmap": [
      "app/services"
    ]
  }
```
然后运行 `composer dump-autoload`。

#### 遵循 psr-4 的项目（如 Laravel 5、Symfony）中：

无需配置，保证目录 `App/Services` 和命名空间 `namespace App\Services;` 一致即可自动加载。

### 使用

```php
use App\Services\OSS;

// 在外网上传一个文件并指定 options 如：Content-Type 类型
// 更多 options 见：https://github.com/johnlui/AliyunOSS/blob/master/src/oss/src/Aliyun/OSS/OSSClient.php#L142-L148
OSS::publicUpload('bucket', '目标 object 名', '本地文件路径', [
    'ContentType' => 'application/pdf',
    ... ...
]);
```