# Wide Area Network Technologies

Let's say that you're in charge of the network as the sole IT support specialist at a small company. At first, the business only has a few employees with a few computers in a single office. You decide to use nonwritable address space for the internal IPS because IP addresses are scarce and expensive. You set up a router and configure it to perform NAT. You can figure a local DNS server and a DHCP server to make network configuration easier. And of course for all of this to really work, you sign a contract with an ISP to deliver a link to the Internet to this office, so your users can access the web. Now imagine the company grows. You're using nonwritable address space for your internal IPs, so you have plenty of space to grow there. Maybe some sales people need to connect to resources on the land you've set up while they're on the road. So you configure a VPN server and make sure the VPN server is accessible via port forwarding. Now, you can have employees from all over the world connect to the office LAN. Business is good and the company keeps growing. The CEO decides that it's time to open a new office in another city across the country. Suddenly, instead of a handful of salespeople requiring remote access to the resources on your network, you have an entire second office that needs it. This is where Wide Area Networks or WAN technologies come into play. Unlike a LAN or a Local Area Network, WAN stands for Wide Area Network. A Wide Area Network acts like a single network, but spans across multiple physical locations. WAN technologies usually require that you contract a link across the Internet with your ISP. This ISP handle sending your data from one site to the other. So it could be like all of your computers are in the same physical location. A typical LAN setup has a few sections. Imagine one network of computers on one side of the country and another network of computers on the other. Each of those networks ends at a demarcation point which is where the ISPs Network takes over. The area between each demarcation point and the ISP's actual core network is called a local loop. This local loop would be something like a T carrier line or a high speed optical connection to the provider's local regional office. From there, it would connect out to the ISP's core network and the Internet at large. WANs work by using a number of different protocols at the data link layer to transport your data from one site to another. In fact, these same protocols are what are sometimes at work at the core of the Internet itself instead of our more familiar ethernet. Covering all the details of these protocols is out of the scope of this course.