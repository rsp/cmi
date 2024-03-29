![Call me irresponsible if I ever crash on null or undefined in JavaScript or TypeScript](title.png)

---

# Rafał Pocztarski

You may know me from Stack Overflow

[<img alt="rsp on Stack Overflow" src="https://stackexchange.com/users/flair/303952.png" height="116">](https://stackoverflow.com/users/613198/rsp)

# pocztarski.com

<small>(and also from Medium, Quora, etc.)</small>

---

Few days ago...

<a href="https://www.quora.com/profile/Rafa%C5%82-Pocztarski">
![Quora followers](rsp-quora-404-followers-a.png)
</a>

My reaction: WTF?! Why I don't have followers?!

---

# Call me irresponsible

if I ever crash on null or undefined<br>in JavaScript or TypeScript

---

# Call me irresponsible

if I ever crash on null or undefined<br>&nbsp;

---

# Call me irresponsible

if I ever crash<br>&nbsp;

---

<i>
Call me irresponsible, call me unreliable<br>
Throw in undependable, too<br>
Do my foolish alibis bore you?<br>
Well, I'm not too clever, I just adore you
</i>

a song about irresponsible software development<br>composed by Jimmy Van Heusen<br>with lyrics by Sammy Cahn

---

Who has ever designed a network protocol?

---

Who has ever been in a dialog like this?

<br><i>"Can you add ID to GET /users/me endpoint?"</i>

<br><i>"OK, it will be &nbsp;`userId`&nbsp; field in JSON"</i>

---

Discussing REST endpoints<br>is designing a network protocol

---

A simplified* model of a typical protocol stack

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

A simplified simplified model of a typical stack

<small>
client's implementation of our custom REST API<br>
(several layers in between)<br>
server's implementation of our custom REST API
</small>

---

We are designing a network protocols<br>so we need to know:

<small>

- RFC 1122: Requirements for Internet Hosts - Communication Layers
- RFC 1123: Requirements for Internet Hosts - Application and Support

</small>

---

<small>

"Software should be written to deal with every conceivable error, no matter how unlikely"

"the most serious problems in the Internet have been caused by unenvisaged mechanisms triggered by low-probability events"

"if a protocol specification defines four possible error codes, the software must not break when a fifth code shows up"

</small>

---

Robustness principle

"Be liberal in what you accept,<br>and conservative in what you send"

---

Robustness principle

"Be conservative in what you send"
<br><small>(your code should always produce correct data)</small>

"Be liberal in what you accept"
<br><small>(your code must never crash when receiving incorrect data)</small>

---

Robustness principle
<br>for a typical RESTful API consumer and provider

<small>

The frontend must always send proper request with correct data
<br>(but if it doesn't then the backend cannot crash!)

The backend must always send proper response with correct data
<br>(but if it doesn't then the frontend cannot crash!)

</small>

---

<small>

When Jackie Gleason was singing about "foolish alibis" in the "Call me irresponsible" song, what he meant was a situation like this:

Backend crashes and the backend developer blames the frontend:

"It's the fault of frontend developers because they sent me a bad request!"

Frontend crashes and the frontend developer blames the backend:

"It's the fault of backend developers because they sent me a bad response!"

</small>

---

![JS error console](irresponsible-console-2-r3.png)

---

NULL is called a billion dollar mistake by its inventor not without a reason

In JavaScript we have both `null` and `undefined` so we are twice as lucky

---

Developer about frontend crashing in production because of getting null from the backend:

"please do not accuse car engine if you pour the wrong kind of gas."

---

![Dashboard](engine-malfunction-s.jpg)

---

![Car](car-explosion-s.jpg)

---

<small>
This worked when `c` was missing but crashed when `b` was missing
</small>

```
x = a.b.c || 'default';
```

---

<small>
This never crashes:
</small>

```
x = _.get(a, 'b.c', 'default');`
```

---

<small>

How to make sure that it's impossible to make a mistake like this

</small>

---

Use TypeScript with maximally restricted config

---

TypeScript

```
{
  "compilerOptions": {
    "noImplicitAny": true,
    "noImplicitThis": true,
    "alwaysStrict": true,
    "strictNullChecks": true,
    "strictFunctionTypes": true,
    "strictPropertyInitialization": true,
    "noImplicitReturns": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true
  }
}
```

---

TSLint

```
{
  "rules": {
    "no-any": true,
    "no-null-keyword": true
  }
}
```

---

TypeStrict

TSLint config focused on maximizing type safety

---

Data validation

<small>

- All data coming from outside should be validated before use
- The application must not crash on unexpected data

---

NULLs

<small>

- Whenever any data can be NULL (or undefined or nonexistent) you have to test it before you use it
- You can use type systems of languages like TypeScript to catch all NULL-related bugs in the compile time

</small>

---

Type systems

<small>

- Use static type systems whenever you can
- Make the type system as restricted as possible if it is configurable like e.g. in TypeScript
- If the type system can catch NULLs then use it to do it
- If the type system can catch missing or incorrect data then use it to do it
- If the type system can exclude null/undefined from all types by default then always exclude it
- If you use a static type system like Flow or TypeScript and you get a type error exception at runtime (TypeError: Cannot read property 'x' of null), you are not using the type system correctly

---

Static analysis

<small>

- Use tools for static analysis of your code
- Use linters with maximum restrictions designed to catch common mistakes
- Make sure that all static analysis errors are corrected and enforced by CI

</small>

---

The application cannot crash

There are no exceptions

---

<small>

- This includes getting data that you don't expect
- This includes getting wrong types of data, wrong size of data, no data, errors instead of data
- When any code crashes it needs to be fixed
- Blaming the conditions that led to crashing (like bad data, someone entered password that is too long, database returned empty result etc.) does not lead to robust software

</small>

---

"You don't handle an exception here"

"But this will almost never happen"

"Yes, that's why it's called <i>exception</i>"

<small>
(my actual conversation in a commercial project)
</small>

---

Resources

<small>

- [RFC 1122: Requirements for Internet Hosts - Communication Layers](https://tools.ietf.org/html/rfc1122)
- [RFC 1123: Requirements for Internet Hosts - Application and Support](https://tools.ietf.org/html/rfc1123)
- [Robustness principle on Wikipedia](https://en.wikipedia.org/wiki/Robustness_principle)
- [Covariance and contravariance on Wikipedia](https://en.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science))

</small>

---

Tools

TypeScript,
TypeStrict,
ts-essentials,
fp-ts,
TSLint,
Airbnb JavaScript Style Guide,
Airbnb TSLint Config,
Prettier,
Ramda,
Immutable.js,
Lodash,
Lodash-FP,
Hoek,
Joi,
Fantasy Land Specification,
Crocks,
Sanctuary

---

Services

TravisCI,
CircleCI,
Snyk,
Codacy,
Code Climate,
Codecov,
Coveralls,
Rultor,
Codebeat,
SonarQube,
AppVeyour,
Codeship

---

# Questions?

Slides: https://pocztarski.com/cmi

## Rafał Pocztarski

## [pocztarski.com](https://pocztarski.com)

“Be liberal in what you accept, and conservative in what you send.” - Postel's law
