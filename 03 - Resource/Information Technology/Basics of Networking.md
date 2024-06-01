# Basics of Networking

When most people think of the Internet, they think of a magical cloud that lets you access your favorite websites, shop online, and you assumingly endless stream of cat pictures, but there isn't any magic involved. There's no mysterious entity that grants us a cat picture on-demand. The Internet is just an interconnection of computers around the world, like a giant spider web that brings all of us together. We call the interconnection of computers a network. Computers in a network can talk to each other and send data to one another. You can create a simple network with just two computers. In fact, you might already have your own network at home connecting all of your home devices. Let's think on a bigger scale. What about the computers at your school or workplace? Are they in a network? They sure are. All of the computers there are linked together in a network. Can we link your home, school, and workplace's networks together? We absolutely can. Your workplace connects to a bigger network, and that network connects to an even bigger network and on and on. Eventually, you've got billions of computers that are interconnected, making up what we call the Internet. You, like most people, probably access the Internet through a browser like Mozilla Firefox, Google Chrome, Microsoft Edge, or something else. This is done through the World Wide Web. But don't make the mistake of thinking the Internet is the World Wide Web. The Internet is the physical connection of computers and wires around the world. The web is the information on the Internet. We use it to access the Internet through a link like www.google.com. The World Wide Web isn't the only way we can access the Internet. Your email, chat, and file-sharing programs are also ways you can access the Internet. In the IT field, managing, building, and designing networks is known as networking. Networking is a super important and large field in IT. There are specialized jobs, college degree programs, and tons of literature dedicated entirely to networking. If you work in the IT field, it's super critical that you understand the fundamentals of networking. The Internet is composed of a massive network of satellites, cellular networks, and physical cables buried underneath the ground. We don't actually connect to the Internet directly. Instead, computers called servers connect directly to the Internet. Servers store the websites that we use, like Wikipedia, Google, Reddit, and BBC. These websites serve content. The machines that we use, like our mobile phones, laptops, video game consoles, and more are called clients. Clients request the content like pictures, websites from the servers. Clients don't connect directly to the Internet. Instead, they connect to a network run by an Internet service provider or ISP, like CenturyLink, Level 3, Comcast, Telefonica and things like that. ISPs have already built networks and run all the unnecessary physical cabling that connects millions of computers together in one network. They also connect to other networks and other ISPs. These other networks connect to the networks of Google, Reddit, universities, basically all the other networks in the world. Together, they form one giant network of computers called the Internet. But how do the clients know how to get to servers? Well, how would you send a letter to someone? You'd put your address on the letter and send it to the address of the person you're sending the letter to. Computers have addresses just like houses. Computers on a network have an identifier called an IP address. An IP address is composed of digits and numbers like 100.1.4.3. When we want to access a website, we're actually going to their IP address, like 172.217.6.46. Devices that can connect to a network have another unique identifier called a MAC address. MAC addresses are generally permanent and hard-coded onto a device. A sample MAC address can be something like this 82:4f:23:59:47:4. When you send or receive data through a network, you need to have both an IP and a MAC address. You might be wondering why we need to have two different numbers to identify something. That's a good question. Think again of the letter analogy we use before. An IP address is your house address, while the MAC address is the name of this recipient of the letter. You want to make sure your letter gets to the right location and to the right person. A more simplified example of the letter delivery would go like this. I'm in New York city and I got a letter that I want to send to a friend, May. May's halfway across the world in Tokyo. Our letter, we'll go through lots of places before it reaches her. I put her name and address on there and I also put my name and address on there too. When I drop my letter off at the post office, the mail person looks at it. He thinks, I don't know how to get to Tokyo from here, but there's a truck that's headed to Texas. He puts my letter in that truck at the post office in Texas. A mail person looks at the letter and says, I don't know how to get to Tokyo from here, but we have a truck going to San Francisco. She puts my letter in that truck. At the post office in San Francisco, yet another mail person looks at my letter. He says, there's a plane headed to Tokyo and puts the letter on that plane. When it finally reaches Tokyo, the postman there says, I know where May lives and delivers the letter to her. Obviously, there are many more nuance to mail delivery than what I described, but this process is similar to how information gets routed across the Internet. One thing to call out is that data that's sent through a network is sent through packets. There's little bits of data and you guessed it, ones and zeros. It doesn't matter if it's pictures, email, music, or text. When we move data through the network, we break them down into packets. When a packet gets to its destination, it will rearrange itself back in order. Think of a packet like a letter. Let's actually look at this process again, but this time we'll use IP addresses and MAC addresses. Natalie has a computer with IP address 113.8.81.2 and she wants to go to google.com and search for pictures of cats. Before she does that, her computer has to send a packet to ask google.com if it can access their website. Our packet knows google.com's IP address is 172.217.6.46, but it doesn't know how to get there just yet. The packet travels from one place to another at each destination where it asks, hey, do you know where google.com is? Eventually it'll be routed to another destination that can get the packet closer and closer to google.com. Once it reaches a destination that can deliver the packet to aserver@google.com, Google will send Natalie a packet saying she can access an unlimited number of cat pictures.
