code

```
import random
import asyncio
 
async def get_menus():
    delay_minutes = random.randrange(3) #0 to 3 minutes
    await asyncio.sleep(delay_minutes) #Pretend a second is a minute
 
async def get_order():
    delay_minutes = random.randrange(10)
    await asyncio.sleep(delay_minutes)
    order = random.choice(['Special of the day', 'Fish & Chips', 'Pasta'])
    return order
 
async def prepare_order(order):
    delay_minutes = random.randrange(10, 20) #10 to 20 minutes
    await asyncio.sleep(delay_minutes)
    print('   [Order ready from kitchen: ', order, ']')
 
async def eat():
    delay_minutes = random.randrange(20, 40)
    await asyncio.sleep(delay_minutes)
 
async def get_payment():
    delay_minutes = random.randrange(10)
    await asyncio.sleep(delay_minutes)
 
async def serve_table(table_number):
    await get_menus()
    print('Welcome. Please sit at table', table_number, 'Here are your menus')
    order = await get_order()
    print('Table', table_number, 'what will you be having today?')
    await prepare_order(order)
    print('Table', table_number, 'here is your meal:', order)
    await eat()
    print('Table', table_number, 'here is your check')
    await get_payment()
    print('Thanks for visiting us! (table', table_number, ')')
 
#Create coroutines for three tables
gathered_coroutines = asyncio.gather(
    serve_table(1),
    serve_table(2),
    serve_table(3)
)
 
#asyncio uses event loops to manage its operation
loop = asyncio.get_event_loop()
#This is the entry from synchronous to asynchronous code. It will block
#Until the coroutine passed in has completed
loop.run_until_complete(gathered_coroutines)
#We're done with the event loop
loop.close()
```

output:

```
Welcome. Please sit at table 1 Here are your menus
Welcome. Please sit at table 2 Here are your menus
Welcome. Please sit at table 3 Here are your menus
Table 1 what will you be having today?
Table 2 what will you be having today?
Table 3 what will you be having today?
   [Order ready from kitchen:  Special of the day ]
Table 2 here is your meal: Special of the day
   [Order ready from kitchen:  Fish & Chips ]
Table 1 here is your meal: Fish & Chips
   [Order ready from kitchen:  Pasta ]
Table 3 here is your meal: Pasta
Table 2 here is your check
Table 1 here is your check
Thanks for visiting us! (table 2 )
Table 3 here is your check
Thanks for visiting us! (table 1 )
Thanks for visiting us! (table 3 )
```