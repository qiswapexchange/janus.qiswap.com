# janus.qiswap.com

## Deployment instructions

1. Configure NGINX with http support

```
cd nginx/conf.d
mv default.conf default.conf.ssl
mv default.conf.http default.conf
```

2. Start docker containers

```
docker-compose up -d
```

3. Create Diffie-Hellman key

```
cd /nginx/
mkdir dhparam
cd dhparam
sudo openssl dhparam -out dhparam-2048.pem 2048
```

4. Restart NGINX with support for https and domain name janus.qiswap.com

```
cd nginx/conf.d
mv default.conf default.conf.http
mv default.conf.ssl default.conf
docker restart nginx
```

4. Add automatic SSL renewal in `cron`

```
sudo crontab -e
```

Add the following line

```
...
0 12 * * * /home/sammy/node_project/ssl_renew.sh >> /var/log/cron.log 2>&1
```