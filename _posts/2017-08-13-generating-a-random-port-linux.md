---
title: Choosing a port for your new TCP server
tags: [linux]
---

Every time I create a new server, One of most painful tasks I need to worry about is choosing the right port for the server. Although every internet system has a space for 65535 TCP ports, with the increasing amount of applications, most of the ports are already occupied either [officially](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml){:target="_blank"} or [unofficially](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers){:target="_blank"}. 

That leaves us with the question of how do you come up with a *free* port number for our server. Well, before we jump right into the solution, here are some ground rules we can follow:

- The port numbers for 1-1024 are reserved for processes running with root privileges on linux. 
- Of the remaining ports, IANA officially recommends the range 49152-65535 for ephemeral ports while some of the unix & windows systems use the range 1024-5000 for the same. <sup>[1](#footnote1)</sup>
- While it is *mostly* safe to use to ports ranging from 5000-49152, given the fact that most well-known services choose to go with smaller port numbers that range around 8000, it’s a good port range to avoid.
- That’s leaves you with a range of ports between 10000 and 49152.

Now, coming to the solution, here’s a little bash snippet that helps you identify a *random* *unused* port on your machine.

    curl -sSL https://git.io/v7Hch | bash

If you’re curious to know what’s happening inside the snippet above, here’s the link to the [repo](https://github.com/v1shwa/random-port-generator){:target="_blank"} on github.


**Footnotes:**

<small id="footnote1"> 1 : [The Ephemeral Port Range ](http://www.ncftp.com/ncftpd/doc/misc/ephemeral_ports.html){:target="_blank"}</small>
