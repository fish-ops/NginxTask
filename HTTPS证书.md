## 通过配置HTTPS加密证书

安装certbot之后，它可以帮我们生成加密证书，然后通过nginx配置。

```bash
$ sudo certbot --nginx

#禁用自动配置，不过没必要
$ sudo certbot --nginx certonly
```

它会
1. 检索nginx配置文件，查找部署在当前机器上的域名
2. 通过DNS解析验证用户合法性，然后生成证书
3. 自动配置nginx配置文件


```
server {
  listen 80;
  server_name mb.bitfish.xyz;
  location / {
    # as a static file
    root /var/www/MessageBoardVue;
    index index.html ;
 }

    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/mb.bitfish.xyz/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/mb.bitfish.xyz/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

}
```

