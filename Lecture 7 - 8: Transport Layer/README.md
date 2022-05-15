# Transport Layer
### Content Table :
- [**What is transport layer ?**](#Whatis)
	- [**The 5-Tuple**](#5-Tuple)
- [**UDP**](#UDP)
- [**CheckSum Method**](#Checksum)
	- [**Sender**](#Sender)
	- [**Receiver**](#Receiver)
- [**TCP**](#TCP)
	- [**Characteristic**](#TCP-CHAR)
	- [**TCP-Header**](#TCP-Header)
	- [**Maximum Segment Size**](#MSS)
	- [**TCP Sequence number and Acks**](#TCP-SEQ)
	- [**TCP Functionality**](#TCP-CE)
		- [Establish Connection](#TCP-F-EC)
		- [Close Connection](#TCP-F-CC)
		- [DC](#TCP-F-DC)
	- [**TCP Preference**](#TCP-PREF)

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
- [**Feature**](#UDP-feature)
- [**Adventage/Disadventage**](#UDP-DA)
- [**UDP-Header**](#UDP-Header)

### How does UDP work?
**UDP** uses **IP** to get datagram ( Link Layer ) from one computer to another. UDP work by adding its own header to packet, [*In figure 1*](#UDP-Header-Diagram).

> **Note :** Unlike TCP, UDP doesn't guarantee the packets will get to the right destinations. This means UDP doesn't connect to the receiving computer directly, which TCP does.

### <a name="UDP-DA"></a> - Adventage/Disadventage of UDP

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

### <a name="UDP-Header"></a> - UDP header 
![UDP-Header](https://www.imperva.com/learn/wp-content/uploads/sites/13/2019/01/UDP-packet-1024x375.jpg)
*<a name="UDP-Header-Diagram"></a>Firgure 1 : UDP Header diagram*

Header Size (8 byte)
- srcPort ( 16 bit )
- dstPort ( 16 bit )

Payload size:

- Min: 0 Byte
- Max: 65,527 byte

### <a name="UDP-feature"></a> - Feature

-   It allows packets to be dropped and received in a different order than they were transmitted, making it suitable for real-time applications where latency might be a concern.
-   It can be used for transaction-based protocols, such as DNS or Network Time Protocol.
-   It can be used where a large number of clients are connected and where real-time error correction isn't necessary, such as gaming, voice or video conferencing, and streaming media.

## <a name="Checksum"></a> Computing Checksum

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

![TCP-Diagram](https://uc358cd72f524f89ef94e839dfa6.previews.dropboxusercontent.com/p/pdf_img/ABh2LZJZJT9osqAtFBhEhsIPVz4_sIZN97Q1-y5-PoUhv0QckJ5t3KRugEe1QcJ2pecYyL_Enjha4-fbChkVkdNmqmmqO3nDDDykMvTBJpriB-fvWoK_QN05d9QKXfod55OSsLwhSY9C50A_WO5AiLWkIJWiJNEatU9K-ZdWbLKFiPVnzGxLHZK1qmhiumMmddym8oT3p37wii6zLB15PW17d53BzS_NYDICOg6RPKqWHbP4ZI3EeUXTJfWq9N52zIgbjxjSngoPoT95KkGLaFrba5t9CfRGglyZ_G0qtSsYs_oomwlG7h8v0hnA_hS-MMbIyiZ1ITdlpfTYJ6IapbEq8SmqDxI2Cys2fcyhXNCe853w5hD-TKLSFYO8f_wxfdFJPs65F0GIf_Sp6HpLPiUl/p.png?page=18&scale_percent=0)
*<a name="TCP-TD"></a>Figure 2: TCP Diagram*

- [**Characteristic**](#TCP-CHAR)
- [**TCP-Header**](#TCP-Header)
- [**Maximum Segment Size**](#MSS)
- [**TCP Sequence number and Acks**](#TCP-SEQ)
- [**TCP Functionality**](#TCP-CE)
	- [Establish Connection](#TCP-F-EC)
	- [Close Connection](#TCP-F-CC)
	- [DC](#TCP-F-DC)
- [**TCP Preference**](#TCP-PREF)

### <a name="TCP-CHAR"></a>  - Characteristic of TCP
TCP is transportation protocol that concern about reliability. This make TCP include :

 - [x] Full Duplex
	 - Bidirection Transmission.
 - [x] Handshaking
	 - Acknowledgement : If B want to send Acks to A it can **attach act to one of the package.**

### <a name="TCP-Header"></a> -  TCP Header
![TCP-Header-DIagram](https://uc358cd72f524f89ef94e839dfa6.previews.dropboxusercontent.com/p/pdf_img/ABh2LZJZJT9osqAtFBhEhsIPVz4_sIZN97Q1-y5-PoUhv0QckJ5t3KRugEe1QcJ2pecYyL_Enjha4-fbChkVkdNmqmmqO3nDDDykMvTBJpriB-fvWoK_QN05d9QKXfod55OSsLwhSY9C50A_WO5AiLWkIJWiJNEatU9K-ZdWbLKFiPVnzGxLHZK1qmhiumMmddym8oT3p37wii6zLB15PW17d53BzS_NYDICOg6RPKqWHbP4ZI3EeUXTJfWq9N52zIgbjxjSngoPoT95KkGLaFrba5t9CfRGglyZ_G0qtSsYs_oomwlG7h8v0hnA_hS-MMbIyiZ1ITdlpfTYJ6IapbEq8SmqDxI2Cys2fcyhXNCe853w5hD-TKLSFYO8f_wxfdFJPs65F0GIf_Sp6HpLPiUl/p.png?page=22&scale_percent=0)
*Figure 3: TCP header diagram*

### <a name="MSS"></a> -  Maximum Segment Size
Inorder for two host to communicate, the must agree on acceptable packet size which specify by **MTU ( Maximum Trasmission Unit )**.

Two Side Must :
 - [x] **Announce Acceptable Packet Size**

>**Note :** General MSS size is 1500 bytes **( Max Ethernet values )**

MTU is already **include TCP and IP headers** which take up **40 bytes** make the real MSS of 1500 **MTU is 1460.**

### <a name="MSS"></a> -  TCP Sequence Number and Acks

**Seq** : Byte stream number of the first byte in segment’s data
**ACKs** Seq# of the next byte expected from the other side 

As TCP is meant to be reliable, if data is collided or loss. TCP will retransmit the data again using ACKs feature.

**Retransmission Situation :**
1. [Lost Segment](#TCP-LS)
2. [UnACK'd](#TCP-UA)
3. [Premature Timeout](#TCP-PT)
4. [Lost Ack](#TCP-LA)

![TCP Sequence Diagram](https://uc358cd72f524f89ef94e839dfa6.previews.dropboxusercontent.com/p/pdf_img/ABh2LZJZJT9osqAtFBhEhsIPVz4_sIZN97Q1-y5-PoUhv0QckJ5t3KRugEe1QcJ2pecYyL_Enjha4-fbChkVkdNmqmmqO3nDDDykMvTBJpriB-fvWoK_QN05d9QKXfod55OSsLwhSY9C50A_WO5AiLWkIJWiJNEatU9K-ZdWbLKFiPVnzGxLHZK1qmhiumMmddym8oT3p37wii6zLB15PW17d53BzS_NYDICOg6RPKqWHbP4ZI3EeUXTJfWq9N52zIgbjxjSngoPoT95KkGLaFrba5t9CfRGglyZ_G0qtSsYs_oomwlG7h8v0hnA_hS-MMbIyiZ1ITdlpfTYJ6IapbEq8SmqDxI2Cys2fcyhXNCe853w5hD-TKLSFYO8f_wxfdFJPs65F0GIf_Sp6HpLPiUl/p.png?page=23&scale_percent=0)
*Figure 4: TCP Sequence Diagram*
#### <a name="MSS"></a> 1. Lost Segment
This happend when one of the segment is **lost during tranportation**. In this case, sender will only need to resend a missing segment start from mission segment to receiver.

The **ACKs** `Host B` return when segment is missing are **duplicated**  **ACKs** of the latest sucess segment.

>**Hint :** `Host A` will retransmit Seq 100,120,140 according to [*figure 5*](#TCP-LS-D)
>
![TCP Lost Segment Example](https://uc358cd72f524f89ef94e839dfa6.previews.dropboxusercontent.com/p/pdf_img/ABh2LZJZJT9osqAtFBhEhsIPVz4_sIZN97Q1-y5-PoUhv0QckJ5t3KRugEe1QcJ2pecYyL_Enjha4-fbChkVkdNmqmmqO3nDDDykMvTBJpriB-fvWoK_QN05d9QKXfod55OSsLwhSY9C50A_WO5AiLWkIJWiJNEatU9K-ZdWbLKFiPVnzGxLHZK1qmhiumMmddym8oT3p37wii6zLB15PW17d53BzS_NYDICOg6RPKqWHbP4ZI3EeUXTJfWq9N52zIgbjxjSngoPoT95KkGLaFrba5t9CfRGglyZ_G0qtSsYs_oomwlG7h8v0hnA_hS-MMbIyiZ1ITdlpfTYJ6IapbEq8SmqDxI2Cys2fcyhXNCe853w5hD-TKLSFYO8f_wxfdFJPs65F0GIf_Sp6HpLPiUl/p.png?page=24&scale_percent=0)
*<a name="TCP-LS-D"></a> TCP Lost segment Example Diagram*

#### <a name="TCP-UA"></a> 2. UnACK'd
No **ACKs** is return. Problem are, it does not know either **packet loss or ACKs lost.**

It will wait for **timeout** and resend again

#### <a name="TCP-PT"></a> 3. Premature Timeout

![enter link description here](https://uc358cd72f524f89ef94e839dfa6.previews.dropboxusercontent.com/p/pdf_img/ABh2LZJZJT9osqAtFBhEhsIPVz4_sIZN97Q1-y5-PoUhv0QckJ5t3KRugEe1QcJ2pecYyL_Enjha4-fbChkVkdNmqmmqO3nDDDykMvTBJpriB-fvWoK_QN05d9QKXfod55OSsLwhSY9C50A_WO5AiLWkIJWiJNEatU9K-ZdWbLKFiPVnzGxLHZK1qmhiumMmddym8oT3p37wii6zLB15PW17d53BzS_NYDICOg6RPKqWHbP4ZI3EeUXTJfWq9N52zIgbjxjSngoPoT95KkGLaFrba5t9CfRGglyZ_G0qtSsYs_oomwlG7h8v0hnA_hS-MMbIyiZ1ITdlpfTYJ6IapbEq8SmqDxI2Cys2fcyhXNCe853w5hD-TKLSFYO8f_wxfdFJPs65F0GIf_Sp6HpLPiUl/p.png?page=27&scale_percent=0)

#### <a name="TCP-LA"></a> 4. Lost ACKs
- LostACK := know by the return ACKs is not duplicate after loss ACKs
```
Send Seq = 100,120,140,160
Received ACKs = 100, --,140, 160

This identicate that the package is recieved because the third ACKs return 
as expected
```

### <a name="TCP-CE"></a> - TCP Functionality
- [Establish Connection](#TCP-F-EC)
- [Close Connection](#TCP-F-CC)
- [DC](#TCP-F-DC)
#### Establish Connection <a name="TCP-F-EC"></a>
Using **SYN** Flag `set SYN = 1` and `seq=client_init_seq` ( Random ).

```
Client --> Server
---------------------
SYN 1 ----> Server // Sent Connection Req
SYN 1 <---- Server // Ackownledge Connection
SYN 0 ----> Server // Start Connection

Threeway Handshake
```

#### Closing Connection <a name="TCP-F-CC"></a>
`Client` send **FIN**  `FIN` to `server` and `server` will return **ACKs** back with **FIN** Flag back again on another package

```
Client --> Server
----------------------
FIN ----> Server // Sent Close Connection Request
ACK <---- Server // Ackownledge FIN
FIN <---- Server // Client Receive FIN
ACK ----> Server // Close connection
Connection Closed
```
>**Note :** TCP only allow server to close half of the connection.

#### Data Control <a name="TCP-F-DC"></a>
- **How fast** data travel. `Flow Control`
	To prevent sender to send data faster than receiver can be processing.
	- Buffer is Full
	- **Overflow**
	- ![Casdasdasda](https://uc358cd72f524f89ef94e839dfa6.previews.dropboxusercontent.com/p/pdf_img/ABh2LZJZJT9osqAtFBhEhsIPVz4_sIZN97Q1-y5-PoUhv0QckJ5t3KRugEe1QcJ2pecYyL_Enjha4-fbChkVkdNmqmmqO3nDDDykMvTBJpriB-fvWoK_QN05d9QKXfod55OSsLwhSY9C50A_WO5AiLWkIJWiJNEatU9K-ZdWbLKFiPVnzGxLHZK1qmhiumMmddym8oT3p37wii6zLB15PW17d53BzS_NYDICOg6RPKqWHbP4ZI3EeUXTJfWq9N52zIgbjxjSngoPoT95KkGLaFrba5t9CfRGglyZ_G0qtSsYs_oomwlG7h8v0hnA_hS-MMbIyiZ1ITdlpfTYJ6IapbEq8SmqDxI2Cys2fcyhXNCe853w5hD-TKLSFYO8f_wxfdFJPs65F0GIf_Sp6HpLPiUl/p.png?page=35&scale_percent=0)
	- `LastByteSent - LastByteAck =< rWindow`

>**Note :** Larger the `rWindow` the lager data can be sent.

- **How much** data sent. `Congestion Control`
	**Congestion Control** is used when there are too many source in network traffic.
	- Package Loss
	- Long Delay
	
	It Was Limited by **Congestion Window** `cWindow`
	- `LastByteSent - LastByteAck =< cWindow`

Thus sender can send data using
`LastByteSent - LastByteAck =< min{ cWindow, rWindow}`

### <a name="TCP-PREF"></a> - TCP Preference for sending rate

- [Slow Start](#TCP-PREF-SS)
- [Conjection Avoidance / Fast Recovery](#TCP-PREF-CA)

**Preferences**
 - [x] Not too fast
 - [x] Not too slow

**Principle**

- Packet lost (timeout / duplicate ACKs) implies congestion, thus sending rate should be decreased
- Arriving ACKs means the network is delivering the packets perfectly, the sending rate can be increased
- Bandwidth probing: The sender keeps increasing the sending rate until packet loss occurs, then back off from that rate and begins to probe again

#### Slow Start <a name="TCP-PREF-SS"></a>
**Increase sending rate exponentially** untill first loss event happen
The exponential will stop when reaching `ssthreshold`

If **lost event** occure at `cWindow = k` TCP sets `ssthreshold = k/2`

#### Congestion Avoidance / Fast Recovery <a name="TCP-PREF-CA"></a>
- TCP enters fast recovery when 3 duplicate ACKs are encountered
- This indicates that the network is still capable of data transmission–ACK’dsegment is corrupt or lost–But 3 other segments arrive correctly
- In this state, instead of resetting the cWindowback to 1 MSS, is cWindowset to the new ssthreshold
![asd](https://uc358cd72f524f89ef94e839dfa6.previews.dropboxusercontent.com/p/pdf_img/ABh2LZJZJT9osqAtFBhEhsIPVz4_sIZN97Q1-y5-PoUhv0QckJ5t3KRugEe1QcJ2pecYyL_Enjha4-fbChkVkdNmqmmqO3nDDDykMvTBJpriB-fvWoK_QN05d9QKXfod55OSsLwhSY9C50A_WO5AiLWkIJWiJNEatU9K-ZdWbLKFiPVnzGxLHZK1qmhiumMmddym8oT3p37wii6zLB15PW17d53BzS_NYDICOg6RPKqWHbP4ZI3EeUXTJfWq9N52zIgbjxjSngoPoT95KkGLaFrba5t9CfRGglyZ_G0qtSsYs_oomwlG7h8v0hnA_hS-MMbIyiZ1ITdlpfTYJ6IapbEq8SmqDxI2Cys2fcyhXNCe853w5hD-TKLSFYO8f_wxfdFJPs65F0GIf_Sp6HpLPiUl/p.png?page=45&scale_percent=0)