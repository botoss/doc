Generic scheme of interactions:

```
                    --------------
                    |            |
                    |  Messenger |
                    |            |
                    --------------
                      |        ^
                      v        |
                    --------------
                    |            |
                    |  Connector |
                    |            |
                    --------------
                      |        ^
                      v        |
 -------------------------   ----------------------------
 |                       |   |                          |
 | Kafka topic to-module |   | Kafka topic to-connector |
 |                       |   |                          |
 -------------------------   ----------------------------
                      |        ^
                      v        |
                    --------------
                    |            |
                    |   Module   |
                    |            |
                    --------------
```

Now, definitions from this scheme:
**Messenger** -- some platform, using which users send commands to our bot and then receive responses from it (vk, telegram, facebook, etc.).
**Kafka topic** -- software component, which can save some messages in form of key-value from data producers, and then send them on requests by multiple data consumers.
**Connector** -- component, which runs in such cycle:
  1. Receive command from messenger.
  2. Send it to module via Kafka topic to-module.
  3. Receive response to command from module via Kafka topic to-connector.
  4. Send it back to messenger.
**Module** -- component, which runs in such cycle:
  1. Receive command from connector via Kafka topic to-module.
  2. Send response to connector via Kafka topic to-connector.

So, connector doesn't know any concrete information about modules, and module doesn't know any information about connectors.

There might be any number of both connectors and modules.

When connector receives command from messenger, it encodes this command into key-value representation to send it into topic to-module.
Scheme:
key -- is any string, generated by connector
value -- JSON of such format:
```
{
  "connector-id": optional string, we haven't decided, do we really need it,
  "command": string, means user command,
  "params": array of strings, which are args of command, possibly null or empty
}
```

Every module takes this message, handles it and responses with such scheme:
key -- same key, as in request to module
value -- JSON:
```
{
  "connector-id": optional string, same as in request,
  "text": string
}
```

Module may decide to not handle message, then it shouldn't respond with anything.
