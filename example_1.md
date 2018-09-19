### code:

```sh
import asyncio
import time

async def compute_sum(x, y):
    print("Compute %s + %s ..." % (x, y))
    await asyncio.sleep(1.0)
    return x + y

async def compute_div(x, y):
    print("Compute %s / %s ..." % (x, y))
    await asyncio.sleep(3.0)
    return x / y

async def print_sum(x, y):
    result = await compute_sum(x, y)
    print("%s + %s = %s" % (x, y, result))

async def print_div(x, y):
    result = await compute_div(x, y)
    print("%s / %s = %s" % (x, y, result))

async def main():
    task1 = loop.create_task(print_sum(1, 2))
    task2 = loop.create_task(print_div(3, 4))
    await asyncio.wait([task1, task2])

if __name__ == '__main__':
    start = time.time()
    loop = asyncio.get_event_loop()
    loop.run_until_complete(main())
    loop.close()
    end = time.time()
    print('total time: {}'.format(end - start))
```

### output

```sh
Compute 1 + 2 ...
Compute 3 / 4 ...
1 + 2 = 3
3 / 4 = 0.75
total time: 3.0041325092315674
```
