# Troubleshooting OpenStack-Ansible

Troubleshooting OpenStack issues can sometimes be a hassle in the environment
that OpenStack-Ansible deploys, because things are not always running where you
might think they're running. This guide covers some basic steps to help narrow
down what the problem might be.

This guide assumes that you have encountered some sort of reproducible issue
while working with OpenStack. If you cannot yet reproduce the issue, then
troubleshooting will be pretty difficult.

## HAProxy

First, to figure out what service is causing the error, check the HAProxy logs.
They will show what requests are being made to the cluster, and which backend
services the requests are being proxied to. A good way to do this is to tail
the logs, watch for a few seconds so you know which requests are probably just
normal background traffic that you can ignore.

TODO: tail command

Once you're ready, while tailing the HAProxy logs as shown above, reproduce the
issue that errors and watch which requests are made. The logs should tell you
which backend container the requests are being forwarded to. Make a note of
these containers - in the next step, we'll check them out.

## Service Containers

Once you have determined which containers are recieving requests, pick one and
attach to it so we can troubleshoot it.

TODO: lxc-attach command

First, check if any systemd services have failed. On the containers, all
services should be functioning properly and in a non-failed state.

TODO: list failed units command

- redo the thing
- haproxy
- container's logs
- possibly other service