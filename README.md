# mosh-with-jump

## Summary

mosh-with-jump is a [Mosh](https://mosh.org) wrapper that supports a single
jump/proxy server like `ssh -J $jump_server`. It does so by starting
`mosh-server` on the target server via the jump server and then proxying UDP
packets through the proxy server.

## Examples

Using a jump server

    ./mosh-with-jump -J $jump_server $destination

Using a jump server with a specific SSH port

    ./mosh-with-jump -S 2022 -J $jump_server $destination

With ports specified (for the target server)

    ./mosh-with-jump -p 61000:61100 -J $jump_server $destination

With all options specified

        ./mosh-with-jump -S 2022 -p 61000:61100 -J $jump_server $destination

Using no jump server (just calls `mosh`)

    ./mosh-with-jump $destination

## Requirements

mosh-with-jump was written with some portability in mind and uses some fairly
common Unix utilities. All machines involved must have [SSH](https://www.openssh.com/). Only the client and
target machines need to have Mosh. The proxy server uses [socat](http://www.dest-unreach.org/socat) to proxy and [ss](https://linux.die.net/man/8/ss)
to query for in-use ports.
