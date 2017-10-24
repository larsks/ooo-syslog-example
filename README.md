This repository demonstrates the use of a sidecar container to proxy
syslog messages from haproxy to stdout.

When using a log *socket* (i.e., when not logging over UDP), the
`chroot` keyword causes some complications: HAProxy logs both before
and after the `chroot`, and a path available outside the `chroot`
won't be available inside the `chroot`.

I've solved that here by mounting the sockets volume twice, on both
`/sockets` and `/var/lib/haproxy/sockets`; this ensures that the log
socket is available on `/sockets/log` both before and after the
`chroot` operation.

An alternate solution would be to configure haproxy to send log
messages to the sidecar using UDP.  Instead of:

    log /sockets/log local2

You would simply use:

    log haproxy-sidecar local2

The rsyslog image is configured to support either mechanism.
