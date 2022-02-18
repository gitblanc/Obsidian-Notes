# OSI Model
There are 7 layers:
#### 7. Application
Provides networking options to programs running on a computer.
#### 6. Presentation
Recieves data from the applications layer. Translates this data into a standardised format.
#### 5. Session
Tryies to set up a connection with other computer across the network. If it can't be, it sends an error and the process goes no further. If a session is established, the session layer maintains it and cooperates with the session layer of the other computer.
####  4. Transport
First chooses the protocol over which the data is to be transmitted. Most common are TCP (Tansmision Control Protocol) and UDP (User Datagram Protocol).
- With TCP, the transmission is **_connection based_** which means that a connection between the computers is stablished and maintained for the duration of the request. This allows for a reliable transmission, as the connection can be used to ensure that the packets **_all_** get to the right place. All lost data is re-sent and the connection is constant.
- With UDP, data can be lost, but is fastest (In Skype sometimes the video is pixelated).
TCP is used in situacions where accuracy is favoured over speed, and USP where speed is more important.
With a protocol selected, the transport layer then divides the transmission up into bite-sized pieces, which makes it easier to trasmit the message succesfully (TCP-segments, UDP-datagrams).
#### 3. Network
Locates the destination of the request. The most common form of logical adressing is the IPV4 (e.g 192.168.1.1).
#### 2. Data Link
Focuses on the physical addressing of the transmission and presents the data in a format suitable for transmission. It recieves a packet from the network layer  (includes the IP of the remote computer) and adds in the physical adress (MAC) of the recieving endpoint. Inside every network enabled computer is a Network Interface Card (NIC) which comes with a unique MAC (Media Access Control) address to identify it.
MAC can't be changed, although they can be _spoofed_. When information is send across the network, it's actually the physical address that is used to identify where exactly to send the information.
It alzo checks that the information transmitted hasn't been corrupted, which could happen in layer 1, the physical layer.
#### 1. Physical
Is right down to the hardware of the computer. Converts the binary data of the transmission into signals and transmit them across the network, as well as receiving incoming signals and converting them back into binary data.

---

# Encapsulation
Process that increases security, preventing data manipulation.
The encapsulated data has different names in layers. 7,6,5 is called data; 4 is called segment/datagram; 3 is called packets; 2 is called frames and 1 is called bits.
When the message is recieved by the second computer, it reverses the process. This is referred as de-encapsulation.
This is useful because is a standardised way to transmit data that is used in all computers, so all transmissions will follow the same methodology.

---

# TCP/IP Model
Consists of four layers, wich cover the same range of functions as the seven layers of the OSI Model..
TCP means Transmission Control Protocol. It's a connection based protocol. You must first form a stable connection between the two computers. This process is called _the three way handshake_.
Whe you attempt to make a connection, your computer first sends a special request to the remote server indicating that it wants to initialise a connection. This request contains a SYN bit (synchronise bit), which makes first contact in starting the connection process. The server will then respond with a packet containing the SYN bit, as well as the acknowledgement bit, called ACK. Finally, your computer will send a packet that contains the ACK bit, confirming that the connection has been set up succesfully. With the three-way handshake succesfully completed, data can be reliabky transmitted between the two computers. Any data that is lost or corrupted is re-sent, so the conection is lossless.

---

# Ping


