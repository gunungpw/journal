# Supplemental Reading for Routing Protocol Examples

We’ve covered a few different routing protocol types, but we haven’t discussed the details of how the actual implementation of these protocols might matter.

Many network protocols are implemented based on specifications published by the [Internet Engineering Task Force (IETF)](https://www.ietf.org/). We'll cover this in more detail in a future lesson!

The most common distance vector protocols are [RIP, or Routing Information Protocol](https://en.wikipedia.org/wiki/Routing_Information_Protocol) ([IETF RFC2453](https://tools.ietf.org/html/rfc2453)), and [EIGRP, or Enhanced Interior Gateway Routing Protocol](https://en.wikipedia.org/wiki/Enhanced_Interior_Gateway_Routing_Protocol) ([Cisco documentation](https://www.cisco.com/c/en/us/support/docs/ip/enhanced-interior-gateway-routing-protocol-eigrp/16406-eigrp-toc.html)). The most common link state protocol is [OSPF, or Open Shortest Path First](https://en.wikipedia.org/wiki/Open_Shortest_Path_First) ([IETF RFC2328](https://tools.ietf.org/html/rfc2328)).

In terms of exterior gateway protocols, there is only one in use today. The entire Internet needs to agree on how to exchange this sort of information, so a single standard has emerged. This standard is known as [BGP, or Border Gateway Protocol](https://en.wikipedia.org/wiki/Border_Gateway_Protocol) ([IETF RFC4271](https://tools.ietf.org/html/rfc4271)).