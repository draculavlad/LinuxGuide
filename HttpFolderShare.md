# NgxCloudStorage

* nginx version 1.6.3

# a quick appoach with python
* host current dir as your http file storage root path
* performance issue
* do not support multi-user scenario
```
python -m SimpleHTTPServer 80
```


# on centos 7

```shell
yum install nginx -y
```

# congifuration of nginx

```properties
# For more information on configuration, see:
#   * Official English Documentation: http://nginx.org/en/docs/
#   * Official Russian Documentation: http://nginx.org/ru/docs/

user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

events {
    worker_connections 1024;
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 2048;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;

    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  _;
#        root         /usr/share/nginx/html;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
 		root         /opt/share;
		autoindex on;
        	autoindex_exact_size off;
        	autoindex_localtime on;
    dav_methods PUT DELETE MKCOL COPY MOVE;

    create_full_put_path  on;
    dav_access            group:rw  all:r;
            allow all;		
        }

#        error_page 404 /404.html;
#            location = /40x.html {
#        }

#        error_page 500 502 503 504 /50x.html;
#            location = /50x.html {
#        }
    }
}
```

# create share folder

```shell
su - root
cd /opt 
mkdir share
chmod 777 share
```

# start

```shell
systemctl start nginx
#after configuration
nginx -s reload
```

# How To Upload File With CURL


* multipart

```shell
curl -v 'http://shadow.elendil.io/dependency-reduced-pom.xml' \
-X PUT -H 'Origin: chrome-extension://hgmloofddffdnphfgcellkdfbfbjeloo' \
-H 'Accept-Encoding: gzip, deflate, sdch' \
-H 'Accept-Language: zh-CN,zh;q=0.8,en;q=0.6' \
-H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/48.0.2564.82 Safari/537.36' \
-H 'Content-Type: multipart/form-data; boundary=----WebKitFormBoundarykArk1ZnuguYAqCci' \
-H 'Accept: */*' \
-H 'Connection: keep-alive' \
--data-binary \
$'------WebKitFormBoundarykArk1ZnuguYAqCci\r\nContent-Disposition: form-data; name="fileUpload"; filename="dependency-reduced-pom.xml"\r\nContent-Type: text/xml\r\n\r\n\r\n------WebKitFormBoundarykArk1ZnuguYAqCci--\r\n' --compressed
```

* simple

```shell
curl -v --upload-file ~/tmp 'http://localhost/'
```
