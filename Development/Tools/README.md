## Linux

```ShellSession
# find PID with searching
$ps -ef | grep {process name}

# open files limit upgrade ( * stands all user except root)
sudo vi /etc/security/limits.conf
*       soft    nofile    65536
*       hard    nofile    65536
root    soft    nofile    65536
root    hard    nofile    65536
```

## Docker

```ShellSession
$sudo apt install docker.io
$sudo usermod -aG docker ubuntu
$sudo service docker start
```

```ShellSession
- Dockerfile
# if requirments.txt differ from cache
RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt
```
`$ docker build -t {name} .`

## Redis

- `set password --requirepass {password}`

```ShellSession
$docker pull redis

$docker run --name some-redis -d -p 6379:6379 redis
$docker run -d -p 6379:6379 -v {redis.conf folder path}/:/usr/local/etc/redis/ --name myredis redis redis-server /usr/local/etc/redis/redis.conf

- run docker redis-cli
$docker exec -it {redis container name} redis-cli
password: redis-cli --askpass

- RDB Save ERROR
>config set stop-writes-on-bgsave-error no
```
- Redis Stream
  - Storage + Pub Sub
  - using websocket `asyncio.gather(ws_send, ws_receive)`