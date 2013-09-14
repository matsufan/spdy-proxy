SPDY Proxy
==========

Reference implementation in [Go](http://golang.org/) of a barebones SPDY/HTTPS proxying server for (semi-)permanently connected back-end servers.

Thanks to Jamie Hall, David Anderson and Derrick McKee for their help and contributions to how this proxy server idea and implementation.

This project is an extracion from a larger Amahi project and Jamie did this code based on a description of how the Amahi project was architected. It uses Jamie's excellent [SlyMarbo/spdy](https://github.com/SlyMarbo/spdy/) SPDY library.

Intro
=====

This is a proxy server process P and a back-end client for it C.

The proxy P serves (on two ports) a client (front-end) API to , called H.

The C (server) is a client that connects to P semi-permanently. Once it's connected, H calls are proxy'd to C, with TLS and SPDY, with C becoming a server for H. 

Once H ends the connection, C's SPDY connection is kept and reused for any other calls with H. Each call from H is funnelled to C via a SPDY stream.

	H	Proxy clients
	^
	|
	v
	P	Proxy
	^
	|
	v
	C	Client device that semi-permanently connect to P, then become Servers for H

Both the server to H and the interface with C support SPDY.

(C) 2013, Amahi
