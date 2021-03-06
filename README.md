# Gotunnel #

### localtunnel with WebSocket support ###

Gotunnel makes your localhost server accessible on the net.

Assuming your server is running on port 3000, on your laptop. Run
`./client -p "3000"` (from the checkedout repository, see [installation](#installation)) and that would make it accessible on a subdomain
at localtunnel.net.

    $ ./client -p 3000
    Setting Gotunnel server localtunnel.net:34000 with local server on 3000

    Connect to vxyz.localtunnel.net

The server is running on ec2 small instance, so although free, might
not be able to handle much load. You can deploy the server on your own
machine (ec2 instance etc), and connect the client to it. More
below.<link>

### How is it different from the original [localtunnel](http://progrium.com/localtunnel/)?

It supports HTTP/S and **WebSocket**. And, more of a technical difference, works by
forwarding connections at TCP level.

## Installation ##
If you are on Mac OS X, just checkout the repository. The client
binary that comes with the repo, should work.

    git clone https://github.com/ciju/gotunnel

If you are on some other OS, or the above didn't work. First [install
Go](http://golang.org/doc/install). Then clone the repo, and build the
client. Ex:

    git clone https://github.com/ciju/gotunnel
    go build client.go

## Client Options ##
    $ ./client
    Usage: ./client [OPTIONS]

    Options:
      -p="": port
      -r="localtunnel.net:34000": the remote gotunnel server host/ip:port
      -sub="": request subdomain to serve on

## Running your own server ##
Install golang, and compile the server with command.

    go build server.go

Run the server with custom options.
    Usage: ./server [OPTIONS]

    Options:
      -a="localtunnel.net": the address to be used by the users
      -p="32000": Access the tunnel sites on this port.
      -x="0.0.0.0:34000": Port for clients to connect to

## Limitations ##

- If making connections to ports like 34000 are not allowed by your
n/w then the client might not work.

- Connection pooling might not be possible. Working at the TCP level,
we loose the ability of knowing when an HTTP/S or websocket request
has finished, except when TCP connection ends.

## TODO ##
- statistics
- better error handling
- make it faster

## LICENSE ##
MIT

**Sponsored by [ActiveSphere](http://activesphere.com)**
