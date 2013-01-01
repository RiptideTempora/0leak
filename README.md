Zeroleak
=====
Desktop and mobile app for zerobin and other encrypted pastebin-like software

How it will work
=====
1. Select your drop server (0bin.net, et al.) and/or add a server to the list
	a. Note: It should cache the public keys of these servers after the first use and alert you if they have changed
2. Type/paste your data into a textbox
3. Do one of the following:
	a. Supply an encryption key
	b. Press the "random" button which will generate a cryptographically secure pseudorandom key
4. Select whether or not to use a SOCKS proxy (i.e. Tor) for the deposit (and other config options)
5. Push button, receive bacon (I mean URL)
	i. Internally, our client will connect to an API (TODO: Write API, send to zerobin author via git) and after verifying the public key of the server, will send the cyphertext (base64-encoded)
	ii. If the cyphertext server API will respond with a URL that contains the index of the pastebin. The key must NOT be transmitted
	iii. The client receives the URL and validates it with a regex similar to ^https:\/\/$server_name\/$stuffWillGoHere

Motivation
=====
Paranoid cryptography nerds (<3 u all :D) will complain about how services like zerobin rely on host-based security and if the host is compromised (either at the CA level or at a server level) then all anonymity and confidentiality goes down the toilet. There's also the issue of Javascript code delivery and the potential of a compromised server exploiting the end user.

With a consistent open-source client for PCs (Windows, Mac, Linux, BSD, etc.) and mobile phones (if needed; low priority), the code delivery risk is eliminated (read the code just to be sure though). With a cache of public keys and built-in paranoia if it changes abruptly, a rogue certificate authority will have a harder time slipping a bad cert under the radar. (Still not impossible though.) With SOCKS, you can tunnel traffic over SSH or Tor and not reveal your real IP address.
