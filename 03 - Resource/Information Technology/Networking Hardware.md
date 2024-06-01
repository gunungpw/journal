# Networking Hardware

Now that we understand what networks are. Let's talk about how they're connected. There are a lot of ways you can connect computers to a network, we'll only cover a few of the major ones in this course. First, there's an ethernet cable which lets you physically connect to the network through a cable. On the back of the desktop we worked in the previous lessons, there's a network ports that you plug your ethernet cable into. Another way to connect to a network is through Wi-Fi, which is wireless networking. Most modern computing systems have wireless capabilities like mobile phones, smart televisions and laptops. We connect to wireless networks through radios and antennas. The last method will go over uses fiber optic cables to connect to a network. This is the most expensive method since fiber optic cables allow greater speeds than all the other methods, fiber optic gets its name because the cables contain glass fibers that move data through light instead of electricity. This means that we send ones and zeros through a beam of light instead of an electrical current through a copper wire. How cool is that? But our cables have to connect to something. We don't just have millions of cables going in and out of computers to connect them together. Instead, computers connect to a few different devices that help organize our network together. The first device that your computer connects to is a router. A router connects lots of different devices together and helps route network traffic, let's say we have four computers, A, B, C and D connected together through a router in the same network. You want to send a file from computer A to computer B. A packets go through the router and the router utilizes network protocols to help determine where to send the packet. So now our packet gets routed from computer A to computer B, sweet. What if we wanted to send a packet to a computer not in our network? What if we wanted to send a packet to our friend Alejandro's computer. Alejandro is on a different network altogether. Fortunately, our router knows how to handle that to the packet will get routed outside our network to our ISPS network using networking protocols, it's able to figure out where Alejandro's computer is. During this process, our packet is traveling across many different routers, switches and hubs, switches and hubs are also devices that help our data travel. Think of switches like mail rooms in a building, routers get our letters to the building, but once we're inside we use the mail room to figure out where to send a letter. Hubs are like company memos, they don't know who to send the memo to, so they send it to everyone. Working with network devices is important to understand because it's likely that one day you'll have users reporting problems accessing the Internet, you'll want to investigate your way up the network stack, a technology stack. In this case a network stack is just a set of hardware or software that provides the infrastructure for a computer. So the network stack is all the components that makes up computer networking. You might need to investigate the network stack in your job. You'd start with making sure the end user computers are working properly. Then you turn your attention to other possible points of failure, like the cabling, switches and routers that work together to access the Internet.