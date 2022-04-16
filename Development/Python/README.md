## FastAPI

- logging
```
- LOCAL
@app.on_event('startup')
async def startup_event():
    logger.setLevel(logging.INFO)
    logHandler = logging.StreamHandler()
    logger.addHandler(logHandler)

- AWS CLOUDWATCH
@app.on_event('startup')
async def startup_event():
    logger.setLevel(logging.INFO)
    logger.addHandler(watchtower.CloudWatchLogHandler(log_group_name="{group_name}", log_stream_name="{stream_name}"))
```


## Celery

- multiprocessing
- CPU intensive
- Redis messaging broker
```
$celery --app celery_task worker -c 6 --loglevel=INFO --logfile=./celery.log
```
