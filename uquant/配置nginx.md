```python
root@asiamiao:/usr/local/nginx# ll
total 36
drwx------ 2 nobody root 4096 Dec 29  2017 client_body_temp
drwxr-xr-x 2 root   root 4096 Sep 29  2018 conf
drwx------ 2 nobody root 4096 Dec 29  2017 fastcgi_temp
drwxr-xr-x 2 root   root 4096 Dec 29  2017 html
drwxr-xr-x 2 root   root 4096 Sep 29  2018 logs
drwx------ 2 nobody root 4096 Dec 29  2017 proxy_temp
drwxr-xr-x 2 root   root 4096 Dec 29  2017 sbin
drwx------ 2 nobody root 4096 Dec 29  2017 scgi_temp
drwx------ 2 nobody root 4096 Dec 29  2017 uwsgi_temp
root@asiamiao:/usr/local/nginx# 
```

```python
/usr/local/nginx/conf#nginx.conf

root@asiamiao:/usr/local/nginx/conf# cat nginx.conf

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
    upstream websocket {
        server 47.93.37.54:3000;
    }

    map $http_upgrade $connection_upgrade {
        default upgrade;
        ''      close;
    }

    server {
        listen       8007;
        server_name  47.93.37.54;

        location /api/push/ws {
            proxy_pass http://websocket;

            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header Host $host;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection $connection_upgrade;
        }


        #location / {
        #    root  /usr/local/nginx/html;
        #    index  index.html index.htm;
        #}

        location ~ .*\.(html|htm|gif|jpg|jpeg|bmp|png|ico|txt|js|css)$
        {
            #root /usr/local/nginx/html/static;
            root /home/riddle/uquant/html;
            #expires      7d; 
        }




        #charset koi8-r;
        #access_log  logs/host.access.log  main;
        #error_page  404              /404.html;
        # redirect server error pages to the static page /50x.html
        #
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
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


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
root@asiamiao:/usr/local/nginx/conf# 


```
