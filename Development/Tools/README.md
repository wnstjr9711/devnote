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
---
## Docker
```ShellSession
*Run docker as none root user*
$sudo apt install docker.io
$sudo usermod -aG docker {NONE ROOT USER}
$sudo service docker start
```
```ShellSession
- Dockerfile

# if requirments.txt differ from cache
RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt

# run as non root user
RUN sudo adduser -u $UID $USER
USER $USER
```
- aws-cli in Dockerfile
  1. Set aws configure as root
  2. Copy /root/.aws/(~/.aws/ in root) -> /home/$USER/.aws/(~/.aws in non-root user)
  3. chown -R $USER /home/$USER/.aws/
  4. USER $USER
---
## Redis
- Single-Threaded(multiple sessions are unnecessary)
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
---
