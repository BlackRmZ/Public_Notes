#### Mysql数据类型

| 说明     | 数据类型             |
| -------- | -------------------- |
| 整数     | int，bit             |
| 小数     | decimal              |
| 字符串   | varchar，char        |
| 日期类型 | date，time，datetime |
| 枚举类型 | enum                 |

1. 字符串
   1. varchar    可变字符串
   2. char    不可变字符串
2. 日期类型
   1. date    日期
   2. time    时间
   3. datetime    日期与时间

#### Mysql字段约束

| 说明     | 约束参数    |
| -------- | ----------- |
| 主键约束 | primary key |
| 非空约束 | not null    |
| 唯一约束 | unique      |
| 默认约束 | default     |

1. 主键约束
   - 区分数据

#### SQL语言的分类

| 简写 | 语义         | 说明                                 |
| ---- | ------------ | ------------------------------------ |
| DQL  | 数据查询语言 | select                               |
| DML  | 数据操作语言 | insert，update，delete               |
| DDL  | 数据定义语言 | create，drop                         |
| TPL  | 事务处理语言 | begin，transaction，commit，rollback |
| DCL  | 数据控制语言 | grant，revoke                        |

#### Mysql数据库服务端启动

1. 查看MySQL服务状态
   - `service mysql status`

2. 停止MySQL服务
   - `service mysql stop`

3. 启动MySQL服务
   - `service mysql start`

4. 重启MySQL服务
   - `service mysql restart`

#### Mysql的配置文件

1. 配置项介绍
   1. port表示端口号，默认3306
   2. bind-address表示服务器绑定的ip，默认为127.0.0.1
   3. datadir表示数据库保存路径，默认为/var/lib/mysql
   4. log_error表示错误日志，默认为/var/log/mysql/error.log