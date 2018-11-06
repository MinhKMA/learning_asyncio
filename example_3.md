```
import asyncio

@asyncio.coroutine
def some_task(name, number):
    print('task ', name, ' started')
    yield from asyncio.sleep(number)
    print('task ', name, ' finished')

@asyncio.coroutine
def loop_executer(loop):
    # you could use even while True here
    while loop.is_running():
        tasks = [
            some_task("A", 2),
            some_task("B", 5),
            some_task("C", 4)
        ]
        yield from asyncio.wait(tasks)

ev_loop = asyncio.get_event_loop()
ev_loop.create_task(loop_executer(ev_loop))
ev_loop.run_forever()
```
