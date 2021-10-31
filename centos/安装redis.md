# 安装redis

1. mkdir /usr/local/shazi/redis

2. mkdir /usr/local/shazi/redis/conf

3. mkdir /usr/local/shazi/redis/data

4. 传入redis-6.2.4至/usr/local/shazi/redis中

5. tar -zxvf redis-6.2.4.tar.gz

6. cd redis-6.2.4

7. make install PREFIX=/usr/local/shazi/redis

8. cp ./redis.conf /usr/local/shazi/redis/conf/

9. sed -i 's/daemonize no/daemonize yes/g' /usr/local/shazi/redis/conf/redis.conf

10. sed -i 's/dir .\//dir \/usr\/local\/shazi\/redis\/data/g' /usr/local/shazi/redis/conf/redis.conf

11. echo "export PATH=/usr/local/shazi/redis/bin:"'$PATH' >> /etc/profile.d/shazi.sh

12. 设置开机启动

``` shell
echo > /etc/systemd/system/redis.service << EOF
[Unit]
Description=redis-server
After=network.target

[Service]
Type=forking
ExecStart=/usr/local/shazi/redis/bin/redis-server /usr/local/shazi/redis/conf/redis.conf
PrivateTmp=true

[Install]
WantedBy=multi-user.target
EOF
```

13. systemctl daemon-reload

14. systemctl enable redis.service

15. systemctl start redis.service
