# 更改301定向

需求: 以前只有.cn域名,现在要兼容.com域名

其实为了SEO,假如baidu.com和baidu.cn域名还有加www和不加www

最好都统一跳到一个url,例如www.baidu.com
这样方便SEO去统计

# Nginx配置

1. 设置配置文件

    ```shell
      6     server_name  xxx.cn www.com;
      7     if ($host != xxx.cn) {
      8         rewrite ^/(.*)$ http://xxx.cn/$1 permanent;
      9     }
    ```
  
  1. permanent: 表示永久重定向到301

2. 校验配置文件正确性: `nginx -t`
3. 重启nginx: `-s reload`

# 参考链接

301参考链接 <http://www.cnblogs.com/benio/archive/2010/08/16/1800584.html>