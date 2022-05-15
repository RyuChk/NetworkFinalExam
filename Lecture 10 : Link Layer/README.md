# Link Layer
### Content Table :
- [What is Link layer ?](#Whatis)
- [Network Adaptor Communication](#NAC)
- [Multiple access Aproaches](#MAA)
	- [Channel Partition Protocol](#CPP)
	- [Random Access Protocol](#RAP)
	- [Taking Turn Protocol](#TTP)
	- [Summary](#MAP-SUM)
- [Network Topology](#NT)
- [Address Resolution Protocol](#ARP)
- [Ethernet](#ETH)

## <a name="Whatis"></a>  Link Layer
Link layer only concern on traporting information from **one node to adjacent ( next ) node**.

- **Node** -- host and router
-   **Links :**
    - Communication channels that connect adjacent nodes along communication path
    - Wired links (LANs)
    - Wireless links (WLANs)
-   **Frame** -- Layer-2 packet that encapsulates datagram
-   **Data-link layer :**
	- responsible for transferring frame from one node to adjacent node over a link
Datagram ( Transport Layer ) are 

>**Note :** Link Network Adaptors Communication

## <a name="NAC"></a>Network Adaptor Communication
**NIC** or network interface card is use and communication adaptor.
- Ethernet card ( LAN )
- Wifi Card
- Bluetooth adaptor

### <a name="LLA"></a>Link-layer Addressing
Link-layer use **MAC-address** , Medium Access Control, to identify devices. Also most of LAN and WLAN ( WIFI ) share the same Mac addressing

 -- **Characterlistic**
- 48 bit address
- All NIC has unique addess

>**Hint :** The addresses will not be exhausted until the year 2100 or later

## <a name="MAA"></a>Multiple Access Approaches
In computer networks, there are three main approaches to manage the multiple access :
1. **Channel Partitioning**
	- [**Time Division Multiple Access**](#TDSM)
	- [**Frequency Division Multiple Access**](#FDSM)
	- [**OTDM/OTDMA**](#OTDM)
2. **Randomly Access**
	- [**ALOHA**](#ALOHA)
	- [**Slotted ALOHA**](#SL-ALOHA)
4. **Coordinating The Access**

## <a name="CPP"></a>Channel Partitioning Protocol
Use a channel-partitioning scheme to divide the channel (multiplexing)

### <a name="TDMA"></a>1. TDMA -- Time Division Multiple Access
Divide by time Frame
- Access channels in rounds
- Each node is assigned with a fixed-length slot
- Unused slots are wasted
- No collision

### <a name="FDMA"></a>2. FDMA -- Frequency Division Multiple Access
Divide by Frequency Band
- Channel spectrum is divided into frequency bands - each node is assigned to a fixed band  
- Unused frequency band is wasted  
- No collision

### <a name="OFDM"></a>3. OFDM/OFDMA 
By combinding FDMA and TDMA we can utilize more slot make data transfer more effecient
-   Some advanced technologies are
		- Orthogonal Frequency Division Multiple (OFDM)       
- Orthogonal Frequency Division Multiple Access (OFDMA)
         - Divide in both frequency and time domains
 - This allows even more bandwidth utilization

### <a name="CDMA"></a>4. CDMA -- Code Division Multiple Access

CDMA : Code Division Multiple Access use code to encrypt data which other cannot read.

Each Node assigned to different unique code.

>**Note :**  In CDMA nodes and continuesly sending data because receiver can distinguish their data by ackownledge sender code.

The Encode Signal is `encoded = ( original data ) x ( chipping sequence )`

>**Note :**  This allow each node to continuesly transmit with minimal interference
>**Hint :**  Used in **3G,4G**
## <a name="RAP"></a> Random Access Protocol

All node transmit without any channel division scheme. If there are **two** or **more** node transmit at the same time the **collision** occurs.

- [**ALOHA**](#ALOHA)
- [**Slotted ALOHA**](#SL-ALOHA)
- [**CSMA, CSMA/CD, CSMA/CA**](#CSMA)

### <a name="TDMA"></a>1. Pure ALOHA
Used in early day at hawai to communicate around island

> **Note :** **Efficiency Rate is only 50%**
-- Channel Efficiency is only **18.5%**

If node frame is send and **collided**, The package will be **back off and resend** at probability of ***P***

### <a name="SL-ALOHA"></a>2. Slotted ALOHA

Pure Aloha with slotted time frame. Each node will send frame at different time and each node will allow to use full frequency.

**Adventage**
- Single active node transmit at full channel capacity
- Decentralized which require **synchronized**
- Simple

**Disadventage**
- Collision Slots are wasted
- Slots Could be wasted after collision
- Require synchronization

### <a name="CSMA"></a>3. CSMA

Improve by applying **sense** which listen to other node before transmit the data. If **collision** is **detected**, stop sending. ( This happend before send )

> **Note :** Even if there are collision is being sense there are still delay which can make collision occure. `Delay = Distance & Propagation Delay`

**CSMA with Collision Detection**
- Detect collision within a very short time
- Abort transmission when a collision is detected to reduce channel waste

## <a name="TTP"></a> Taking Turn Protocol
Take best feature of both random and channel partitioning.

**Adventage of each protocols**
-   **Channel partitioning protocols**
    - Efficient at high loads: share the channel fairly
	- Inefficient at low load: time slots or frequency band are wasted
- **Random access protocols**
    - Efficient at low load: single node can fully utilize the channel
    - Inefficient at high load: collision overhead

### 1. Polling Protocol ( Required Master Node )
**Master** node poll each **Slave** node in round-robin fashion
- No collision is occure
>**Note :** **Master** node need to be **Alive** or the network fails.

### 2. Token Passing Protocol ( Not Required Master Node )
**Passing special token** which allow node to transmit. The token will be passed to next node.
> **Note :** Need to make sure token is being passthrough.

## <a name="MAP-SUM"></a> Media Access Protocol : Summary
- **Channel partition by time, frequency and code**
- **Random access**
   - ALOHA, slotted ALOHA
   - CSMA
   - CSMA/CD: Ethernet
- **Taking turns**
    - Polling protocols: bluetooth
    - Token passing: Fiber Distributed Data Interface (FDDI)

## <a name="NT"></a> Network Topology
- [Bus](#Bus)
- [Ring](#Ring)
- [Start](#Star)

### <a name="Bus"></a>1. Bus Topology
All Device connect same cable
```
   PC1	   PC2	   PC3		//Connected Device
	|		|		|
o--------------------------o 	//Cable
// o = terminator which use to prevent data signal reflect back
```
1. Only **One Device and communication** at a time
2. Data can be tranfer **Bidirectional**

### <a name="Bus"></a>2. Ring Topology
 
Ring Model --> All device are connected in circle.
1. Only **One Device and communication** at a time
2. Data can be tranfer **Bidirectional**
3. Some Protocol **FDDI** which use **token** to organize

![Ring Topology Diagram](https://www.computerhope.com/jargon/r/ring.gif)

### <a name="Star"></a>3. Star Topology
All Device are connect to a switch or hub

1. Data can be tranfer **Bidirectional**
2. Some Protocol **FDDI** which use **token** to organize

## <a name="ARP"></a>Address Resolution Protocol
Use to discovering the link **layer address ( MAC )**, associate with network **layer address ( IP )**.
Each Node will have ARP table which map **MAC address with IP** 

>**Note :** Each Node have TTL

![ARP use case](https://github.com/RyuChk/NetworkFinalExam/blob/main/Lecture%2010%20:%20Link%20Layer/ARP.jpg)

## <a name="ETH"></a>Ethernet

### <a name="MFS"></a>1. Minimum File Size
Ethernet has minimun file size because it need to be ensure that the frames **reach destination** before sender **finish sending frame**.

This is because if the size is too small, the collision will not detect if the package finish the end the connection before frame.

### <a name="EDTS"></a>2. Ethernet Data Transfer Service
1. Connectionless
2. Unreliable
	- CRC happend once each frame
	- No Ack or Nacks.
3. Use CSMA/CD
