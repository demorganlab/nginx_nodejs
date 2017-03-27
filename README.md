
# How to use Nginx with Nodejs Service



### Ubuntu server


editor the file in **/etc/nginx/sites-available/example.dmglab.com**

```sh
#the IP(s) on which your node server is running. I chose port 3000.
#upstream app_yourdomain {
# server 127.0.0.1:3000; is the nodejs service
#keepalive 8;
#}

# the nginx server instance
server {
    listen 0.0.0.0:80;
    server_name example.dmglab.com;
    access_log /var/log/nginx/example.dmglab.com.log;

    # pass the request to the node.js server with the correct headers
    # and much more can be added, see nginx config options
    location / {
        proxy_http_version 1.1;
         proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
         proxy_set_header   X-Forwarded-For $remote_addr;
        proxy_set_header   Host $http_host;
        proxy_pass         "http://localhost:3000"; 
        #set the port of the nodejs service
    }
 }
```
