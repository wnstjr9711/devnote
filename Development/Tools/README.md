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

- run docker redis-cli
$docker exec -it {redis container name} redis-cli

- RDB Save ERROR
>config set stop-writes-on-bgsave-error no
```
- Redis Stream
  - Storage + Pub Sub
  - using websocket `asyncio.gather(ws_send, ws_receive)`