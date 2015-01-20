# PHP开发规范
 
---
## 编码
 
### 命名
 
- 变量名
    驼峰, 首字母小写, eg: `$serviceName`
- 类名
    驼峰, 首字母大写, eg: `class ClassName`
- 方法名
    驼峰, 首字母大写, eg: `function FunctionName`
 
 
### 注释
 
使用**PhpDoc**风格注释
 
### 环境定义
 
```PHP
$env = $app->detectEnvironment(function(){
    if(file_exists(__DIR__ . '/../env.php')) {
        return require __DIR__ . '/../env.php';
    } else {
        return getenv('BC_ENV') ?: 'dev';
    }
});
```
 
### 配置文件
 
- Config目录下建立`dev`, `test`, `preonline`, `online`4个文件夹, 分别放置对应环境的配置文件
- 默认配置文件同**test**环境
    - 可运行
    - 不会产生垃圾数据到生成环境
 
 
---
## 程序结构
 
### 层次
 
- Route 路由
- Controller 控制器类
    - 参数验证
    - 组合数据(调用Biz层)
    - 页面数据
- Bussness 业务逻辑类
    - 调用接口
    - 读写数据库
- Model 表实体类
> 仅当为业务系统, 有库表操作时
 
 
---
## 数据库
 
### 命名
 
- 表名
    下划线, 全小写, eg: `mysql_table_name`
- 字段名
    下划线, 全小写, eg: `mysql_field_name`
- 索引名
    `idx`开头, 以下划线连接主要的字段名, eg: `idx_field1_field2`
 
 
---
## 文件版本管理
 
代码统一使用**Git**
 
### 日常提交
 
### 项目合作
 
- 初始化: 新建项目分支
- 开发中: 合作者共同更新该分支(pull/push)
- 测试时: 合并外部修改(如有必要), 测试环境切换到该分支
- 上线前: 合并外部修改, 复测后代码合并到master
- 上线时: 始终使用master分支上线
 
 
---
## 部署&测试
 
### 主要环境
 
- 开发(dev) 本地开发
- 测试(test) 功能测试
- 预上线(preonline) 预上线测试
- 生产(online)
> 除个别特殊情况外, **严禁**在生成环境进行代码修改及调试操作
 
 
#### 测试环境
 
分为测试环境(test)和预上线环境(preonline)
- 测试环境(test) 使用全套**测试**环境的接口/数据库
- 预上线环境(preonline) 根据情况使用**线上**或**预上线**环境的接口/数据库
 
 
#### 测试环境部署
 
- 整套环境使用 `*.test.baicheng.com`
> 预上线环境将**test**替换为**preonline**
- `*.test.baicheng.com` DNS泛解析到某台Nginx
- Nginx将其全部指向某台内网机器
- 任何新项目直接在该内网机器上部署即可
 
 
---
## 文档
 
文档统一使用**GitLab**的**Wiki**功能
 
主要部分:
- 项目接口文档
- 开发公共包文档
- 开发规范文档
- 开发笔记分享
 
> 具体见Demo `doc.wiki`
