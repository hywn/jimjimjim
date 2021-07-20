# cube demo protocol
this document describe communication protocol of 'cube demo'

## 1. establish connexion
client connect to server at `ws://{host}/chat/{username}`

so, server now can associate the username with the client.

server reject client if username is taken

## 2. server->client messages
server send to client

### 2a. server->client sends 'existance' of all cubes

server sends messages to client informing 'existance' of currently connected cubes (including the client itself)

this is done
1. a new cube connects, so its existance is sent to everyone
2. a new cube connects, so the existances of everyone is sent to it

each 'existance' message is JSON in the form

```
{ type: 'existance', username: string, x: number, y: number, z: number }
```

### 2b. server->client sends 'move'

server sends messages to client informing any new movement of currently connected cubes (including the client itself)

each 'move' message is JSON in form

```
{ type: 'move', username: string, x: number, y: number, z: number }
```

### 2c. server->client sends 'say'

server sends messages to client informing any new 'chat messages' said by connected cubes (including the client itself)

each 'say' message is JSON in form

```
{ type: 'say', username: string, message: string }
```

### 2d. server->client sends 'nonexistance' of a cube
server sends messages to client informing the 'nonexistance' (disconnection) of a currently connected cube.

each 'nonexistance' message is JSON in form

```
{ type: 'nonexistance', username: string }
```

## 3. client->server messages
client sends to server

### 3a. send a 'move'
client send server to inform it wish to 'move' to a new position.

format:

```
{ type: 'move', x: number, y: number, z: number }
```

### 3b. send a 'say'
client send server to inform it wish to 'say' something; send a chat message.

format:

```
{ type: 'say', message: string }
```