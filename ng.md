<!--
 * @Description: In User Settings Edit
 * @Author: your name
 * @Date: 2019-09-25 17:14:47
 * @LastEditTime: 2019-12-04 12:21:44
 * @LastEditors: Please set LastEditors
 -->
### nginx

##### 作用：

1. 反向代理 请求转发给具体的服务器

2. http容器 web Server 处理客户端对静态资源的请求，或者用反向代理将请求转发给tomcat这种服务器

3. 负载均衡(数据流量分发到多台服务器，减轻每台服务器压力)
4. 邮件代理服务器

---
目前静态资源在php_nginx

一般的主入口是：**nginx.conf**

```shell
# 指定执行 worker进程的运行用户
user  nobody;
# nginx 要开启 的进程数
worker_processes  2;
# worker_cpu_affinity 01 11 （每个cpu的核数，二进制）
worker_cpu_affinity auto;

# 日志输出路径 级别
error_log  /var/log/nginx/error.log warn;

# 最多打开文件数限制
worker_rlimit_nofile xxxxx;

events {
    # 多路复用模型
    use epoll;
    worker_connections  xxxxx;
}
http {
  # 限流访问，防止恶意攻击（秒杀） xcsale占用3M，平均每秒1次
  # $binary_remote_addr 客户端IP
  limit_req2_zone $http_uid zone=xcsale:3m rate=1r/s;
}

```

=====

```shell
# 字体文件跨域，：任何域都可以访问；如果不指定，会默认当前域。header 里面会加origin
location ~* "\.(ttf|ttc|otf|eot|woff|font.css)$" {
        add_header 'Access-Control-Allow-Origin' '*';
        add_header 'Access-Control-Allow-Credentials' 'true';
        add_header 'Access-Control-Allow-Methods' 'GET';
    }
```