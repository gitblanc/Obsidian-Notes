# 📘Theory📘
---

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
# 🔋💡TOOLS💡🔋

---
## Ping
It is used to test wether a connection to a remote resource is possible. Uses the ICMP protocol. It can be used to determinate the IP address of the server hosting a website.
````
ping <destination>
````
---
## Traceroute
Maps the path of your request as it heads to the target machine. It allows to see every intermediate step between your computer and the resource that you requested.
````
traceroute <destination>
````

---
## Whois
A domain translates into an IP address so that we don't need to remember it. Whois allows you to query who a domain name is registered to.
````
whois <domain>
````

---
## Dig
An URL gets converted to an IP address with DNS (Domain Name System). DNS gives us the IP address of the website we are trying to access.

You make a request to a website. The first thing that your computer does is check its local cache to see if it's already got an IP address stored for the website; if it does, great. If not, it goes to the next stage of the process.

Assuming the address hasn't already been found, your computer will then send a request to what's known as a _recursive_ DNS server. These will automatically be known to the router on your network. Many Internet Service Providers (ISPs) maintain their own recursive servers, but companies such as Google and OpenDNS also control recursive servers. This is how your computer automatically knows where to send the request for information: details for a recursive DNS server are stored in your router. This server will also maintain a cache of results for popular domains; however, if the website you've requested isn't stored in the cache, the recursive server will pass the request on to a _root name_ server.

Before 2004 there were precisely 13 root name DNS servers in the world. These days there are many more; however, they are still accessible using the same 13 IP addresses assigned to the original servers (balanced so that you get the closest server when you make a request). The root name servers essentially keep track of the DNS servers in the next level down, choosing an appropriate one to redirect your request to. These lower level servers are called _Top-Level_ _Domain_ servers.

Top-Level Domain (TLD) servers are split up into extensions. So, for example, if you were searching for tryhackme**.com** your request would be redirected to a TLD server that handled `.com` domains. If you were searching for bbc**.co.uk** your request would be redirected to a TLD server that handles `.co.uk` domains. As with root name servers, TLD servers keep track of the next level down: _Authoritative name servers_. When a TLD server receives your request for information, the server passes it down to an appropriate Authoritative name server.

Authoritative name servers are used to store DNS records for domains directly. In other words, every domain in the world will have its DNS records stored on an Authoritative name server somewhere or another; they are the source of the information. When your request reaches the authoritative name server for the domain you're querying, it will send the relevant information back to you, allowing your computer to connect to the IP address behind the domain you requested.

When you visit a website in your web browser this all happens automatically, but we can also do it manually with a tool called `dig` .

Dig allows us to manually query recursive DNS servers of our choice for information about domains:
```
dig <domain> @<dns-server-ip>
```

This gives tons of information. If appears `status: NOERROR` we recieved a full answer, which contains the IP address for the domain we required.
Another interesting information is the TTL (Time To Live), which is measured in seconds.