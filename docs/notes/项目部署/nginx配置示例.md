- 打开`nginx-1.24.0/conf/nginx.conf`文件，进行如下配置：

```bash
#user  nobody;
worker_processes  1;
#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;
#pid        logs/nginx.pid;
events {
    worker_connections  1024;
}
http {
    include       mime.types;
    default_type  application/octet-stream;
    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';
    #access_log  logs/access.log  main;
    sendfile        on;
    #tcp_nopush     on;
    #keepalive_timeout  0;
    keepalive_timeout  65;
    #gzip  on;
    server {
        listen       8010;
        server_name  localhost;
        #charset koi8-r;
        #access_log  logs/host.access.log  main;
        location / {
            root   html;
            index  index.html index.htm;
        }
        location /cesiumlab/{
          #自动文件索引功能，默为off。它允许用户直接通过浏览器访问特定的目录，‌而无需上传实际的文件
          autoindex on;
          #计算文件确切大小（单位bytes），off 显示大概大小（单位K、M)，默认on
          #autoindex_exact_size on;
          #显示本机时间而非GMT(格林威治)时间，默认off
          #autoindex_localtime on;
          #允许来自任何域的跨域请求
          add_header Access-Control-Allow-Origin *;
          #为指定的URI创建一个别名路径，‌它允许将请求的URI与文件系统中的实际路径解耦。
          #alias I:/BD/OSGB/3dtiles/;
          alias F:/cmr/z_main/项目/低空组网显控系统/数据/3dtiles/;
          #设置服务器响应的默认字符集为UTF-8
          charset utf-8;
        }
        location /jilantai/ {
          autoindex on;
          add_header Access-Control-Allow-Origin *;
          alias F:/cmr/z_data/吉兰泰镇/;
          charset utf-8;
        }
        #error_page  404              /404.html;
        # redirect server error pages to the static page /50x.html
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }
    # another virtual host using mix of IP-, name-, and port-based configuration
    server {
        listen       8016;
        listen       [::]:8016;
        server_name  target-display  alias  another.alias;
		    location / {
            root   html/target-display/dist;
            index  index.html index.htm;
        }
    }
	  server {
        listen       8017;
        listen       [::]:8017;
        server_name  pg;
		    location / {
            root   html/pg/dist;
            index  index.html index.htm;
        }
    }
	  server {
        listen       8018;
        listen       [::]:8018;
        server_name  ts;
		    location / {
            root   html/ts/dist;
            index  index.html index.htm;
        }
    }
    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}
}
```
