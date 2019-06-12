![Call me irresponsible if I ever crash on null or undefined in JavaScript or TypeScript](title.png)

---

# Rafał Pocztarski

You may know me from Stack Overflow

[<img alt="rsp on Stack Overflow" src="https://stackexchange.com/users/flair/303952.png" height="116">](https://stackoverflow.com/users/613198/rsp)

# pocztarski.com

Enough about me

---
Few days ago

<a href="https://www.quora.com/profile/Rafa%C5%82-Pocztarski">
![Quora followers](rsp-quora-404-followers-a.png)
</a>

My reaction: WTF?! Why I don't have followers?!

---

# Call me irresponsible

if I ever crash on null or undefined<br>in JavaScript or TypeScript

---

# Call me irresponsible

if I ever crash on null or undefined

---

# Call me irresponsible

if I ever crash

---

<i>
Call me irresponsible, call me unreliable<br>
Throw in undependable, too<br>
Do my foolish alibis bore you?<br>
Well, I'm not too clever, I just adore you<br>
Call me unpredictable, tell me I'm impractical<br>
Rainbows, I'm inclined to pursue<br>
Call me irresponsible, yes, I'm unreliable<br>
But it's undeniably true<br>
I'm irresponsibly mad for you
</i>

<small>
a song about irresponsible software development<br>composed by Jimmy Van Heusen<br>with lyrics by Sammy Cahn
</small>

---

Who has designed a network protocol?

---

Who has been in the dialog like this?

Frontend developer:<br><i>I need an endpoint to get user's ID</i>

Backend developer:<br><i>OK, I'll add /users/me</i>

---

A simplified* model of typical protocol stack

<small>
client's implementation of our custom REST API<br>
clients's application layer (HTTP)<br>
client's session/presentation layer (SSL)<br>
client's transport layer (TCP)<br>
client's network layer (IPv4 + NAT)<br>
client's data link layer (Wi-Fi)<br>
client's physical layer (microwaves)<br>
(Wi-Fi access point and several routers in between)<br>
server's physical layer (network cable)<br>
server's data link layer (ethernet)<br>
server's network layer (IPv4)<br>
server's transport layer (TCP)<br>
server's session/presentation layer (SSL)<br>
server's application layer (HTTP)<br>
server's implementation of our custom REST API
</small>

---

<small>
*) The simplified model didn't include:

access points, routers, name servers, proxies, load balancers, content delivery networks, backbones, databases, external services

the same application may work over both IPv4 and IPv6

it can use HTTPS, HTTP/2 and SPDY depending on the connecting client

the API may use REST, GraphQL, gRPC, SOAP, WebSocket

the client itself might be connected over ethernet, Wi-Fi, LTE etc. and even switch network types or cell towers or access points while using the application
</small>

---

A simplified simplified model of typical protocol stack

<small>
client's implementation of our custom REST API<br>
(blah blah blah)
server's implementation of our custom REST API
</small>

---

We are designing a network protocol so we need to know

RFC 1122: Requirements for Internet Hosts - Communication Layers

RFC 1123: Requirements for Internet Hosts - Application and Support

---

Most important excerpts from RFCs 1122 and 1123

"Software should be written to deal with every conceivable error, no matter how unlikely"

"the most serious problems in the Internet have been caused by unenvisaged mechanisms triggered by low-probability events"

"if a protocol specification defines four possible error codes, the software must not break when a fifth code shows up"

---

Robustness principle

Be conservative in what you send
<br><small>(your code should always produce correct data)</small>

Be liberal in what you accept
<br><small>your code must never crash when receiving incorrect data</small>

---

# Questions?

Slides: https://pocztarski.com/cmi

## Rafał Pocztarski

## [pocztarski.com](https://pocztarski.com)

“Be liberal in what you accept, and conservative in what you send.” - RFCs 1122 and 1123
