# Configuring Ubuntu Firewall on my OptiPlex 7090


## Overview
As part of the hardening process on this machine, I am going to enable and configure ubuntu's built-in endpoint firewall. This machine has sensitive data on it, so I'd like for it to be as secure as possible.


I started by running `sudo ss -tulpn` to see what's currently listening on this machine. ss is socket service, and the flags are as follows: -t and -u for TCP and UDP respectively, -l to filter only for what's listening, -p to show what process owns the specific socket, and -n to show port numbers. I'm not going to show the output for security reasons, but luckily it wasn't *too* insecure. 

The main thing to disable was the SSH socket. 
