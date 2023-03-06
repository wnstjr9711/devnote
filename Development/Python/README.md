## FastAPI
- logging
  ```python
  # LOCAL
  @app.on_event('startup')
  async def startup_event():
      logger.setLevel(logging.INFO)
      logHandler = logging.StreamHandler()
      logger.addHandler(logHandler)
  
  # AWS CLOUDWATCH
  @app.on_event('startup')
  async def startup_event():
      logger.setLevel(logging.INFO)
      logger.addHandler(watchtower.CloudWatchLogHandler(log_group_name="{group_name}", log_stream_name="{stream_name}"))
  ```
  ```python
  # Log body of POST requests
  @app.middleware("http")
  async def log(request: Request, call_next):
      try:
          body = await request.body()
  
          async def receive():
              return {'type': 'http.request', 'body': body}
  
          request._receive = receive
          response = await call_next(request)
          if request.url.path != '/':
              logger.info(
                  'address: {}, {} {}?{} body:{} {}'.format(request.headers.get('x-forwarded-for'), request.method,
                                                            request.url.path, request.url.query, body,
                                                            response.status_code))
          return response
      except Exception:
          logger.info(traceback.format_exc())
  ```
- Rate Limiting(Throttling)
  - limit API call per client(ip)
  - redis expire/ttl key
- sqlalchemy
  - sqlalchemy Core + encode/databases
  - connection pool with databases(asynchronous)
- pydantic
  ```python
  # Validate Request Body
  @root_validator()
  def validate_fields(cls, values):
      return values
  ```
---
## Celery
- multiprocessing
- CPU intensive
- Redis messaging broker
```
$celery --app celery_task worker -c 6 --loglevel=INFO --logfile=./celery.log
```
>### receive celery result as task done(asynchronously)
>```python
>import asyncio
>from asgiref.sync import sync_to_async
>
># Converts a Celery tasks to an async function
>def task_to_async(task):
>    async def wrapper(*args, **kwargs):
>        delay = 0.1
>        async_result = await sync_to_async(task.delay)(*args, **kwargs)
>        while not async_result.ready():
>            await asyncio.sleep(delay)
>            delay = min(delay * 1.5, 2)  # exponential backoff, max 2 seconds
>        return async_result.get()
>    return wrapper
>```
