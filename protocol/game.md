# Game Protocol
- UDP-based, unlike other games of similar age.
- UDP suggests that every zone has its own Server.
- Game connects to an entirely different port than is listed anywhere.
- Lack of packet size consistency suggests compression is in use.
    - Age shrinks pool of available compression methods significantly.
    - No consistent header for any packets.
- Game opens two connections:
  - Chat Server
  - Game Server

## Game
### 1. Login Packet (sent at launch)
```
Offset  | Length | Description
--------+--------+----------------
...
x41     | 7      | "061004_"
x48     | ??     | "netver:"
...
x55     | ??     | "didver":
...
x91     | ??     | Subscription Name (UTF-16)
...
xC8     | ??     | Login Token (entire rest of the packet)
```

### Unconfirmed
Guessed Packet Structure:
```
Offset  | Length | Description
--------+--------+----------------
0       | 2      | Identifier
2       | ...    | Data
```

Guessed Packet Identifiers:
```
Id      | Description
--------+----------------
  00 33 | Server Packet, appears when in the north west corner of Stormreach Harbor
  00 3A | Server Packet, appears in Stormreach Market
  02 C4 | Client Packet
  02 5D | Client Packet
```

Packet 02 5D:
```
Offset  | Length | Description
--------+--------+----------------
0       | 2      | Identifier
2       | ...    | Data

```

There's absolutely no consistent data after the first two bytes here, suggesting compression is applied. 

## Chat
Communication is mixed plain text and binary.

### Login Packet (sent at launch, before selecting character)
```
Offset  | Length | Description
--------+--------+----------------
x48     | ??     | "netver:"
...
x55     | ??     | "didver":
...
x91     | ??     | Subscription Name (UTF-16)
...
xC8     | ??     | Login Token (entire rest of the packet)
```

### Incoming Chat Message
```

Length | Description
-------+----------------
...
1      | Username Length in Characters
...... | Username (UTF-16, Zero-Terminated)
18     | ???
1      | Channel Name Length in Characters
...... | Channel Name (UTF-16, Zero-Terminated), if Area chat, Area is surrounded by (), and Channel is split by '+'
2      | x04 x08
4      | Message Length in Characters
...... | Message (UTF-8, Zero-Terminated)
```

Guild 0x0F00000000010228
123456789012345678901234
Oh alright, thanks

