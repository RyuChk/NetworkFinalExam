# Transport Layer
### Content Table :
- [What is transport layer ?](#Whatis)
	- [The 5-Tuple](#5-Tuple)
- [UDP](#UDP)
- [CheckSum Method](#Checksum)
	- [Sender](#Sender)
	- [Receiver](#Receiver)
- [TCP](#TCP)

## <a name="Whatis"></a>  Tansport Layer
Transport layer is layer which consist on how to transport infortaion from host to reciever.

```
*TCP/IP*
Physical --> Link --> network --> Transport --> Application
```

### <a name="5-Tuple"></a>The 5-TUPE
1. Source IP (SrcIP)  -- Network Layer Header
2. Source port (SrcPort) -- **Tranpsport Layer**
3. Destination IP (DstIP) -- Network Layer Header
4. Destination port (DstPort) -- **Transport Layer** 
5. Tranporting Protocol etc, TCP/UDP

> **Note :** Transport layer consist Of **Port** and **IP** 

##  <a name="UDP"></a>UDP (User Datagram Protocol)
### Sub-Table
- [Feature](#UDP-feature)
- [Adventage/Disadventage](#UDP-DA)
- [UDP-Header](#UDP-Header)

### How does UDP work?
**UDP** uses **IP** to get datagram ( Link Layer ) from one computer to another. UDP work by adding its own header to packet.

> **Note :** Unlike TCP, UDP doesn't guarantee the packets will get to the right destinations. This means UDP doesn't connect to the receiving computer directly, which TCP does.

### <a name="UDP-DA"></a> Adventage/Disadventage of UDP

Adventage
```
1. Fast
	- No HandShaking ( Checking Connection between two host )
2. Low overhead
```

Disadventage
```
1. No Congestion Control / Packet Retransmission
2. Did not know who is the sender. 
```

>**Note :** DDOS on UDP happend more easily as reciever not know who is the sender.

Example Usage:
 1. DNS
 2. Shooting / Delay concern games
 3. Video Conference / Livestream

### <a name="UDP-Header"></a> UDP header 
![UDP-Header](https://www.imperva.com/learn/wp-content/uploads/sites/13/2019/01/UDP-packet-1024x375.jpg)

Header Size (8 byte)
- srcPort ( 16 bit )
- dstPort ( 16 bit )

Payload size:

- Min: 0 Byte
- Max: 65,527 byte

### <a name="UDP-feature"></a>Feature

-   It allows packets to be dropped and received in a different order than they were transmitted, making it suitable for real-time applications where latency might be a concern.
-   It can be used for transaction-based protocols, such as DNS or Network Time Protocol.
-   It can be used where a large number of clients are connected and where real-time error correction isn't necessary, such as gaming, voice or video conferencing, and streaming media.

## <a name="Checksum"></a>Computing Checksum

Checksum is a simple error-detection mechanism
>**Hint :**  It is **optional** in **UDP**
- [Sender](#Sender)
- [Receiver](#Receiver)
### <a name="Sender"></a> Sender

#### 1. Divide entire segment into 16 bit words
First dividing the **entire segment** into 16-bit `words`

| 1110011001100110 |  1110011001100110|
|--|--|
| 0000000000001000 |  |

#### 2. Sum all word
Compute the sum of all words

```
1110011001100110 // Word 1
1101010101010101 // Word 2
0000000000001000 // Word 3
+
----------------
1011101111000100 // The sum of all word
```
>**Hint :** Using wraparound method with overflow bit

#### 3. Perform 1st compliment to the sum
```
1011101111000100 // The sum of all word
<-------------->
0100010000111011 // After perform 1st compliment == Checksum
```
In table --
| 1110011001100110 |  1110011001100110|
|--|--|
| 0000000000001000 | 0100010000111011 (Checksum)|
### <a name="Receiver"></a>Receiver

#### 1. Perform sum of received segment

#### 2. Compare The sum with checksum
```
if the condition is **Equal**:
	return No-error
else:
	return ErrorFound
```

Package will be dropped.

## <a name="TCP"></a>  TCP
TCP is a **reliable** and **in-order byte stream**. TCP using pipelined which both sender and receiver have buffers ( Waiting for information to complete before precessing )



