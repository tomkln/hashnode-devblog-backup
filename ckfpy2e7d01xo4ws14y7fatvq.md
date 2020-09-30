## Load Balancing, Geo DNS, or Anycast?

Currently, [Gentlent](https://www.gentlent.com) is built on a proprietary web server that was built with scalability in mind. We always asked ourselves one question: How do we improve performance?

# 1. Load Balancing
We started out with thinking about load balancers and DNS round-robin to distribute traffic across multiple instances in our cluster. Both technologies were implemented to test how it performs. Clearly, it does its job - load balancing requests.

But that’s about it. Visitors are sent to one of our locations, but there’s no effort that they reach a server close to them.

# 2. Geo DNS
We came up with a new possible solution: Geo DNS. If you connect to one of our domains, a DNS server of ours responds with an IP address. We tried using certain technologies to respond with an IP address of a server close to the visitor, which was a little more complicated than we thought:

With the rise of DoH (DNS over HTTPS) provider, requests start to be proxied. Also, the location data may not always be accurate. This may result in visitors reaching servers in locations far away from them, but also sends most of the users to the same far-away location.

# 3. The Networking Way
For most of us, web designers and web developers, the routing part of the internet is a mystery that just works. We looked into it and came up with the best solution yet: Anycast. Anycast means that multiple servers from all around the world are reachable under the same IP address. Therefore, the fastest server closest to you responds to the visitor.

However, there’s some work involved. We had to get at least an IP subnet containing hundreds of IPv4 addresses (/24) which will get more and more expensive as we’re running out of IPv4 space. Due to this very reason, we had to provide a reason for why we should get them. Also, we had to learn about BGP, announcing IPs, had to contact data centers and server providers to allow us to announce them, and join our regional internet registry.

But it works!

# 4. The Future
We want to scale and improve the performance and our services for all of our customers. Therefore, we’ll connect all of the above technologies - software/hardware load balancing, DNS round-robin, GeoDNS, and anycast - to create the best experience possible.

Thanks for reading. Let us know if you’re interested in learning more or want us to get into Anycast hosting for all of you.

