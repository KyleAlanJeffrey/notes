context: https://pypi.org/project/asyncua/

**Description**
A mostly asynchronous python implementation of OPC UA Client/Server api.

*Client Code Snippet
```
from asyncua import Client

async with Client(url='opc.tcp://localhost:4840/freeopcua/server/') as client:
    while True:
        # Do something with client
        node = client.get_node('i=85')
        value = await node.read_value()
```

*Code Examples*
https://github.com/FreeOpcUa/opcua-asyncio/tree/master/examples
