## Docker

```ShellSession
$sudo apt install docker.io
$sudo usermod -aG docker ubuntu
$sudo service docker start
```


## Redis

- `set password --requirepass "{password}"`

```ShellSession
$docker pull redis

$docker run --name some-redis -d -p 6379:6379 redis
$docker run -d -p 6379:6379 -v {redis.conf folder path}/:/usr/local/etc/redis/ --name myredis redis redis-server /usr/local/etc/redis/redis.conf
```
