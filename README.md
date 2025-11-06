# MBBS in Docker

## What

This is the docker-compose file and a description how to create a working MBBS
(Mike's BBS) in Docker running in Dosbox-X

MBBS was THE BBS-software to run in the 90's in Norway , and later ABBS and
BBBS got its inspiration from this piece of software. 

## How to use it

Download the files from this repo, copy MBBS and wanted utilities into the
mbbs-folder. The mbbs folder will be the root of the S: drive in dosbox, so
you should install mbbs into s:/bbs . 

Configure the nodes accordingly to the MBBS 10.4 documentation. All nodes
should be configured with COM1 as a modem, as Dosbox-X emulates a modem on
the comport. 

You could install a fossil driver if you wish. 

How I have it configured is with 7 nodes, and an 8th Dosbox for admin-work
(the window in the middle on the desktop)

Expose port 5000/tcp to the internet with port forwarding (I'm using 1337 ->
5000 ) , using standard port 23 on incoming telnet will most likely result
in a rather unavailable BBS. 

Port 6080 *SHOULD NOT* be exposed directly to the internet, as it is the
console for the BBS. Use http://[your ip]/vnc.html to access it. If you
want VNC directly you could map port 5900 in docker-compose.yml. 

Port 5000 is handled by haproxy which proxies the connection in a load
balancing manner into the Dosboxes. 

The way I have it set up at my home is not with port forwarding in my
firewall, but rather a Pangolin proxy running on a cloud computer, and a
newt tunnel set up in docker-compose.yml where the tcp-connections is
proxied back into my BBS, and it seems to work really well. 


## Known bugs

- I am aware of the telnet client commonly used in linux have some trouble
  with some local echoing that I have not got rid of. Other clients like
syncterm works fine.

