# how to use
## 1. define configuration and call set_logger method to start logging process in main
```
from process_logging.logger import Logger, HandlerType

logger = Logger()
log_fime_name = "{:%Y-%m-%d}_info.log".format(datetime.now())
log_path = "./logs/"
trf_handler_args = {"filename": log_path + log_fime_name,
                    "when": "midnight",
                    "interval": 1,
                    "encoding": "utf-8"}
format_def = ("[%(levelname)s] | %(process)d | %(asctime)s | %(message)s", "%Y-%m-%d %H:%M:%S")
handler_def = {HandlerType.StreamHandler: {}, HandlerType.TimedRotateFileHandler: trf_handler_args}

if __name__ == "__main__":
    logger.set_logger(name="logger", level=logging.INFO, handler_def=handler_def, format_def=format_def)
```

## 2. atfer set _logger, you can logging anywhere in your project with Logger()
```angular2html
@cbv(project_router)
class Router:
    def __init__(self):
        self._logger = Logger()

    @project_router.get(PREFIX)
    def test_func(self):
        # logging
        self._logger.logging(name="logger", level=logging.INFO, message="logging test")
```

## 3. result
```angular2html
[INFO] | 4147 | 2023-08-30 10:09:29 | logging test
```