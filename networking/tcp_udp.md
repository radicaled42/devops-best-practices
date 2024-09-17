# TCP/UDP

TCP creates a secure communication line to ensure the reliable transmission of all data. Once a message is sent, the receipt is verified to make sure all the data was transferred.

UDP does not establish a connection when sending data. It sends data without confirming receipt or checking for errors. That means some or all of the data may be lost during transmission.

Here are the main differences between TCP and UDP:

| **Factor**            | **TCP**                                            | **UDP**                                  |
|-----------------------|----------------------------------------------------|------------------------------------------|
| **Connection type**    | Requires an established connection before transmitting data | No connection is needed to start and end a data transfer |
| **Data sequence**      | Can sequence data (send in a specific order)       | Cannot sequence or arrange data          |
| **Data retransmission**| Can retransmit data if packets fail to arrive      | No data retransmitting. Lost data can’t be retrieved |
| **Delivery**           | Delivery is guaranteed                            | Delivery is not guaranteed               |
| **Check for errors**   | Thorough error-checking guarantees data arrives in its intended state | Minimal error-checking covers the basics but may not prevent all errors |
| **Broadcasting**       | Not supported                                     | Supported                                |
| **Speed**              | Slow, but complete data delivery                  | Fast, but at risk of incomplete data delivery |

## Advantages of TCP

Transmission Control Protocol (TCP) is the protocol to choose for maximum reliability and quality. It may not be the fastest, but it gets the job done right. Here are a few advantages of the TCP protocol:

- It sets up and maintains a connection between sender and receiver.
- It operates independently of the operating system.
- It supports many routing protocols.
- It checks for errors, guaranteeing data arrives at its destination unaltered.
- It confirms data arrival after delivery, or attempts to retransmit.
- It’s able to send data in a particular sequence.
- It optimizes the pace of data transmission based on the receiver.

## Disadvantages of TCP

TCP isn’t suited for some types of data transfers, especially ones that require faster speeds. These are the drawbacks of TCP packet transmission:

- It uses more bandwidth and is slower than UDP.
- It’s especially slow at the beginning of a file transfer.
- It can prevent data from loading if some data is lost. For example, it won’t load images on a web page until all of the page data has been delivered.
- It reduces its transfer rate if the network is congested, resulting in even slower speeds.
- It’s not suited for LAN and PAN networks.
- It can’t multicast or broadcast.

Despite its slower speeds, TCP is the only protocol that can retransmit lost data packets. **When reliability is critical, TCP is the best option**.

## Advantages of UDP

UDP delivers data rapidly, and it doesn’t slow down or turn back to recollect lost data. This makes it an ideal protocol for delivering continuous data or broadcasting, such as for live streaming, video calling, and matching servers with IP addresses. Here are some of the advantages of UDP:

- No connection is needed to send or receive data, so apps and operating systems work faster.
- Broadcast and multicast transmission is available, meaning one UDP transmission can send data to multiple recipients.
- It endures packet loss, delivering data even if it's incomplete.
- Smaller packet size and less overhead reduce end-to-end delay.
- Operates over a larger range of network conditions than TCP.
- UDP communication is more efficient.
- It can transmit live and real-time data.

## Disadvantages of UDP

While UDP provides the speed you need to live a comfortable digital life, UDP isn’t as reliable as TCP. This is something to be aware of when setting up a VPN, because most VPNs run on UDP protocols to keep connection speeds high. Here are some disadvantages of using UDP:

- It’s connectionless, which makes data transfer unreliable.
- There’s no system in place to acknowledge a successful data transfer.
- There’s no way to know if data is delivered in its original state, or at all.
- It has no error control, so it drops packets when errors are detected.
- In case of a data collision, routers will often drop UDP packets and favor TCP packets.
- Multiple users accepting UDP data can cause congestion, and there’s no way to mitigate this.
- It cannot sequence data, so data can arrive in any order or out of order.
