# PHP-Apache 5.6 / 7.4 多环境docker部署

## 安装
```
1. clone 本项目
2. docker-compose up -d
``` 

## 说明
- php5.6 默认为 80 端口
- php7.4 默认为 90 端口
- mysql5.7 默认为 3306 端口
- `conf` 文件夹下为相关配置文件
- `data/mysql` 文件夹为mysql数据文件
-  `logs` 文件夹 为相关日志文件
- `site/www56` 为 php5.6 项目文件夹
- `site/www74` 为 php7.4 项目文件夹